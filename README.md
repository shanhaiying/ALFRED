# Alfred Settings
- Web Bookmarks:  show bookmarks via keyword bm  (works for chrome and safari)
- Calculator : Enable advanced calulator and standard calculator.
- Clipboard double alt, snippet double cmd, Alfred Hotkey double shift.

# Alfred Tips
- We can use SQL like string search in Clipboard search: eg. `pa%das` search `pandas`.
- We can use `cmd s` to save clipboard history content as the snippet.


# Snippet working for substring
> example: Pandas data manipulation
  `df...gri`  expands to `df.groupby([''], as_index=False)['']`.
  Auto Expansion Options check on Expand snippet mid-string.
  

# Replace substring from copied text
```python
import sys
import re
import subprocess

# First create a variable called 'args' from first workflow item and use it in python script.
query = sys.argv[1]
old, new = query.split(' ')

lines = subprocess.check_output('pbpaste').split('\n')
lines = "\n".join([l.replace(old,new) for l in lines])

sys.stdout.write(lines)
```
