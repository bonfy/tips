### DEMO

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
