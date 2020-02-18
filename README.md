# python-iransystem
IranSystem encoding for Python

```python
import iransystem
codecs.register(lambda e: iransystem.getregentry())
```

You may need to reverse decoded characters. for example:

```python
import codecs
import dbfread
import iransystem

def reverse(s):
    return s[::-1]

codecs.register(lambda e: iransystem.getregentry())

# Read Iranian Tamin Ejtema'ee Paradox DBF file
table = dbfread.DBF('DSKWOR00.dbf', encoding='iransystem')

for record in table:
    first_name = reverse(record['DSW_FNAME'])
    last_name  = reverse(record['DSW_LNAME'])
    print('%s %s' % (first_name, last_name))
```
