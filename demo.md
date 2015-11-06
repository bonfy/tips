### DEMO

## Windows open file

usually we do like this:

```python

with open(filename,'w') as f:
    f.write(content)

```
but the windows codec usually is ASCII, will report error
wo we should do like this:

```python
import codecs
with codecs.open(filename,'a','utf-8') as f:
    f.write(content)
```
