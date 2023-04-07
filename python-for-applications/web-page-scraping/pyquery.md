# PyQuery

First, install the pyquery and requests modules:

```bash
python3 -m pip install pyquery
```

Then, we'll get data from the Monash University Wikipedia page's infobox table.

Note that the PyQuery object is like a wrapper around other XML/HTML elements, and that you can find elements using [jQuery selectors](https://www.w3schools.com/jquery/jquery\_ref\_selectors.asp). By default pyquery uses an xml parser then falls back if errors occur, but problems can occur with parsing, so we recommended to use the "html" or "html\_fragments" parser over the default "xml".

```python
import requests
from pyquery import PyQuery as pq

doc = pq(url='https://en.wikipedia.org/wiki/Monash_University', parser='html')
info_table = doc("table.infobox.vcard tbody")[0]

uni_info = {}
for tr_elements in info_table:
    td_and_th_elements = pq(tr_elements)('td, th')
    if len(td_and_th_elements) == 2:
        key_td, value_td = td_and_th_elements
        uni_info[pq(key_td).text()] = pq(value_td).text()

from pprint import pprint
pprint(uni_info)
```

This outputs the following:

```python
{'Academic staff': '8,990 (2019)[5]',
 'Administrative staff': '9,029 (2019)[5]',
 'Affiliations': 'List\n'
                 'Go8\n'
                 'ASAIHL\n'
                 'World Health Summit\n'
                 'John Monash Science School\n'
                 'Monash College',
 'Campus': 'Suburban\n110 hectares (1.1\xa0km2)',
 'Chancellor': 'Simon McKeon AO',
 'Colours': 'Blue, black\n'
            '\n'
            '.mw-parser-output '
            '.legend{page-break-inside:avoid;break-inside:avoid-column}.mw-parser-output '
            '.legend-color{display:inline-block;min-width:1.25em;height:1.25em;line-height:1.25;margin:1px '
            '0;text-align:center;border:1px solid '
            'black;background-color:transparent;color:black}.mw-parser-output '
            '.legend-text{}',
 'Doctoral students': '5,236 (2019)[5]',
 'Endowment': 'A$2.63 billion (2018)[3]',
 'Established': '1958; 64\xa0years ago\xa0(1958)',
 'Location': 'Melbourne\n,\nVictoria\n,\nAustralia',
 'Motto': 'Ancora imparo (Italian)[2]',
 'Motto in\xa0English': '"I am still learning"[2]',
 'Postgraduates': '25,392 (2019)[5]',
 'Students': '86,753 (2019)[5]',
 'Type': 'Public research university',
 'Undergraduates': '55,650 (2019)[5]',
 'Vice-Chancellor': 'Margaret Gardner AC[4]',
 'Website': 'www\n.monash\n.edu'}
```
