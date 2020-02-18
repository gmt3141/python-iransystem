# python-iransystem

Nearly all old Iranian programs (specially programs from golden DOS era) and great number of new enterprise programs have IranSystem encoding. Here is a python module for easy reading and decoding IranSystem encoded files.

## Using module

```python
import iransystem
codecs.register(lambda e: iransystem.getregentry())
```

You may need to reverse decoded strings:

```python
def reverse(s):
    return s[::-1]
```
# Examples

### Example1: Read a text file

```python
import codecs
import iransystem

def reverse(s):
    return s[::-1]

codecs.register(lambda e: iransystem.getregentry())

with open('document.txt', encoding='iransystem') as f:
    for line in f:
        line = ' '.join([reverse(word) for word in line.strip().split()])
        print(line)
```

### Example2: Read a Paradox DBF file

```python
import codecs
import dbfread
import iransystem

def reverse(s):
    return s[::-1]

codecs.register(lambda e: iransystem.getregentry())

# Read an Iranian Tamin Ejtema-ee's Paradox DBF file
table = dbfread.DBF('DSKWOR00.dbf', encoding='iransystem')

for record in table:
    first_name = reverse(record['DSW_FNAME'])
    last_name  = reverse(record['DSW_LNAME'])
    print('%s %s' % (first_name, last_name))
```

## Problems

### Problem with arabic ligature LAM with ALEF «ﻻ»
Reading IranSystem encoded streams works perfectly, but all «ﻻ» (`\ufefb`) characters shown in isolated form. You can replace it with two character sequence LAM + ALEF (`\u0644\u0627`). For example you can replace `reverse` function with:
```python
def iransystem_postproc(s):
    return s[::-1].replace('\ufefb', '\u0644\u0627')
```
### Encoder doesn't work
While decoding from IranSystem works perfectly, encoding to IranSystem doesn't work at all. Maybe I will find spare time for working on it.

## License

Copyright © 2020  [Ghorban M. Tavakoly](mailto:gmt3141@gmail.com)

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program.  If not, see <https://www.gnu.org/licenses/>.
