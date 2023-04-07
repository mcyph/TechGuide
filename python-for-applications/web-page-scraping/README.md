# Web Page Scraping

There are a number of python libraries which are useful for getting data from less complex webpages:

* `beautifulsoup` allows getting data from potentially malformed HTML as usually seen on webpages on the Internet.&#x20;
* `pyquery` provides a similar library for getting data using an interface similar to jQuery for JavaScript.

For more complex cases such as when logins are required or content generated on-demand in client JavaScript applications, a full web browser can be launched and interacted with. This can optionally be "headless", meaning it will render in the background without opening a GUI window.

* `selenium` allows interacting with a real web browser.
