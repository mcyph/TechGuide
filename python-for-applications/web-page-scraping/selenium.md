# Selenium

## Working with Selenium/BrowserMobProxy

First, install the python `selenium`, `browsermobproxy` and `psutil` modules:

```bash
python3 -m pip install selenium psutil browsermobproxy
```

Then, download the Chromium driver corresponding to your installed Google Chrome version from [https://sites.google.com/chromium.org/driver/](https://sites.google.com/chromium.org/driver/).&#x20;

Note that the driver will need to be updated when the web browser on your system updates, as it interacts with the system-installed version externally.

While it is possible to use other engines such as Firefox, we encountered exceptions when interacting with web pages and couldn't get it working beyond a certain point.

```python
import psutil
from selenium import webdriver
from browsermobproxy import Server


BROWSER_MOB_PROXY_LOC = expanduser('~/browsermob-proxy-2.1.4-bin/'
                                   'browsermob-proxy-2.1.4/bin/'
                                   'browsermob-proxy')


def grab(url: str):
    path.append(GECKO_BROWSER_DIR)
    system('killall browsermob-prox')

    # Destroy any previous instances of browsermob-proxy
    for proc in psutil.process_iter():
        if proc.name() in ("browsermob-proxy",
                           "browsermob-prox"):
            print("Killing proc:", proc.name())
            proc.kill()

    print("Creating Server...")
    server = Server(BROWSER_MOB_PROXY_LOC)
    server.start()
    time.sleep(1)

    print("Creating Proxy...")
    proxy = server.create_proxy(params={'port': 9770})
    time.sleep(1)

    print("Creating Selenium/Chrome...")
    args = [
        "--proxy-server=localhost:%s" % proxy.port,
        '--ignore-certificate-errors',
        '--disable-dev-shm-usage',

        '--disable-extensions',
        '--disable-gpu',
        '--no-sandbox',
        '--headless',
    ]
    chrome_options = webdriver.ChromeOptions()
    for arg in args:
        chrome_options.add_argument(arg)
    driver = webdriver.Chrome(options=chrome_options)
    driver.set_window_size(1400, 1050)

    proxy.new_har("file_name", options={
        'captureHeaders': True,
        'captureContent': True,
        'captureBinaryContent': True
    })

    driver.get(url)
    time.sleep(20)
    proxy.wait_for_traffic_to_stop(10, 60)

    item = []
    # print(proxy.har, dir(proxy.har))
    for ent in proxy.har['log']['entries']:
        req = ent['request']

        data = ent['response']['content']['text']
        try:
            data = base64.b64decode(data)
        except: pass
        try:
            data = data.decode('utf-8')
        except: pass
        item.append([req['url'], data])

    server.stop()
    driver.quit()
    return item
```
