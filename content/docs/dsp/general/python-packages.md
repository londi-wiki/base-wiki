---
weight: 999
title: "Python Packages"
description: ""
icon: "article"
date: "2023-10-05T13:40:03+02:00"
lastmod: "2023-10-05T13:40:03+02:00"
draft: false
toc: true
---

- Webframework Packages (django, flask, ..)
- Packages für Bildbearbeitung (Pillow, scikit-images, ..)
- Datenbank ORMs (sqlalchemy, peewee)
- Packages für Webcrawling (scrapy,)
- Numbercrunching (numpy, scipy, pandas)
- Machine Learning (scikit-learn, TensorFlow, PyTorch, ..)
- Datenvisualisierung (matplotlib, altair, bokeh, ..)



## json

```python
import json

some_data = [
    {'object': 'flat', 'sqm': 70, 'location': 'Brugg', 'price': 900000 },
    {'object': 'house', 'sqm': 180, 'location': 'Baden', 'price': 1500000 },
]

# we can directly transform such objects to valid json
json_data = json.dumps(some_data)
```

## serde

[serde](https://pypi.org/project/serde/#getting-started)


## requests

```python
import requests
r = requests.get('http://www.fhnw.ch')

r.status_code # 200
r.encoding # 'utf-8'
r.headers # {'Date': 'Mon, 16 Jan 2023 15:58:50 GMT', 'Server': 'waitress', 'Strict-Transport-Security': 'max-age=300', 'X-Frame-Options': 'SAMEORIGIN', 'X-Content-Type-Options': 'nosniff', 'Cache-Control': 'max-age=0, s-maxage=900, must-revalidate', 'Content-Language': 'de', 'Content-Type': 'text/html;charset=utf-8', 'Expires': 'Fri, 18 Jan 2013 15:58:50 GMT', 'Vary': 'Cookie,Accept-Encoding', 'X-Cache-Operation': 'plone.app.caching.moderateCaching', 'X-Cache-Rule': 'plone.content.itemView', 'X-Varnish': '67087323 58976042', 'Age': '42', 'Accept-Ranges': 'bytes', 'Content-Encoding': 'gzip', 'Content-Length': '7993', 'Keep-Alive': 'timeout=5, max=99', 'Connection': 'Keep-Alive'}

# the first 10 rows of the content
r.content.decode('utf-8').rsplit('\n')[:10]

### ---

data = requests.get(url)

data.content[:1000]


# write the data to a csv file (in binary form)
with open('zh_bevoelkerung.csv', 'wb') as fid:
    fid.write(data.content)
    
# and read it now with pandas from the csv-file
import pandas as pd

df = pd.read_csv("zh_bevoelkerung.csv")

df.head()
```


## scrapy - webcrawling

[HowTo](https://www.digitalocean.com/community/tutorials/how-to-crawl-a-web-page-with-scrapy-and-python-3)


## flask - A Lightweight Web Framework

```python
#!/usr/bin/env python3

import flask

app = flask.Flask('justanexample')

@app.route('/api/this/', methods=['POST'])

def do_reply():
    """
    Function run at each API call
    """
    # reads the received json 
    jsonfile = flask.request.get_json()
    res = dict()
    if jsonfile is None:
        res['this'] = 'nada'
    else:
        for key in jsonfile.keys():
            # calculates and predicts 
            res[key] = 'this'

    # returns a json file 
    return flask.jsonify(res)


if __name__ == '__main__':
    app.run(debug=True)
```

```bash
ls -la flask_example.py
./flask_example.py
```

## rich

```python
from rich import print

print("[italic red]Hello[/italic red] World!", locals())
```

Auch [Tabellen](https://rich.readthedocs.io/en/stable/progress.html?highlight=table#table-columns) können geprinted werden.

## tqdm

Ermöglicht Fortschrittsbalken anzuzeigen

```python
from tqdm import tqdm

for i in tqdm(range(int(9e6))):
    pass
```

# sympy

Formeln anzeigen. [Look here :D](https://docs.sympy.org/latest/tutorials/intro-tutorial/index.html)





