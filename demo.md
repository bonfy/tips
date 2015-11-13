### DEMO


## Windows default is ASCII change to utf-8
```python
import platform
sysstr = platform.system()
if sysstr == 'Windows':
    import sys 
    reload(sys) # Python2.5 初始化后会删除 sys.setdefaultencoding 这个方法，我们需要重新载入 
    sys.setdefaultencoding('utf-8') 

```

## Windows open file

usually we do like this:

```python

with open(filename,'w') as f:
    f.write(content)

```
but the windows codec usually is ASCII, will report error
so we should do like this:

```python
import codecs
with codecs.open(filename,'a','utf-8') as f:
    f.write(content)
```

## logging demo

```python
import logging
import logging.handlers

# setting logging

LOG_FILE = 'tst.log'

formatter = logging.Formatter(
    '[%(asctime)s %(levelname)s %(filename)s:%(lineno)d]: %(message)s'
)

# initialize handler
logger = logging.getLogger('cba')

handler = logging.handlers.RotatingFileHandler(LOG_FILE, maxBytes=1024*1024, backupCount=5)
handler.setFormatter(formatter)
logger.addHandler(handler)

# add stream handler 
handler_stream = logging.StreamHandler() 
handler_stream.setFormatter(formatter)
logger.addHandler(handler_stream)


logger.setLevel(logging.DEBUG)
```

## requests PROXY 的正确打开方式

```python

import urllib
import requests
import random

_usr = 'username'
_pwd = 'xxx###'
_encoded_pwd = urllib.quote_plus(_pwd)

_PROXIES = {
    'http':'http://{usr}:{pwd}@proxy:port'.format(usr = _usr,pwd = _encoded_pwd),
}

USER_AGENTS = ('Mozilla/5.0 (Macintosh; Intel Mac OS X 10.7; rv:11.0) Gecko/20100101 Firefox/11.0',
               'Mozilla/5.0 (X11; Ubuntu; Linux x86_64; rv:22.0) Gecko/20100 101 Firefox/22.0',
               'Mozilla/5.0 (Windows NT 6.1; rv:11.0) Gecko/20100101 Firefox/11.0',
               'Mozilla/5.0 (Macintosh; Intel Mac OS X 10_7_4) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.46 Safari/536.5',
               'Mozilla/5.0 (Windows; Windows NT 6.1) AppleWebKit/536.5 (KHTML, like Gecko) Chrome/19.0.1084.46 Safari/536.5',)


r = requests.get(url, proxies = _PROXIES, headers={'User-Agent': random.choice(USER_AGENTS)} )

```

## get time stamp

``` python
import os
import datetime

def get_stamp():
    """ get time stamp
        :return: string (stamp like '12:00')
    """
    os.environ['TZ'] = 'Asia/Shanghai'
    now = datetime.datetime.now()
    stamp = now.strftime('%H:%M')
    os.environ['TZ'] = 'UTC'
    return stamp
    
```

## python count

``` python
from itertools import count
for page in count(1):
    print page
    if flag:
        return
```
