Table of Contents
=================
   * [Alfred Settings](#alfred-settings)
   * [Alfred Tips](#alfred-tips)
   * [Snippet working for substring](#snippet-working-for-substring)
   * [Replace substring from copied text](#replace-substring-from-copied-text)
   * [Useful Links](#useful-links)

# Alfred Settings
- Web Bookmarks:  show bookmarks via keyword bm  (works for chrome and safari)
- Calculator : Enable advanced calulator and standard calculator.
- Clipboard double alt, snippet double cmd, Alfred Hotkey double shift.

# Alfred Tips
[Alfred Cheatsheet](https://www.alfredapp.com/help/getting-started/cheatsheet/).  
- We can use SQL like string search in Clipboard search: eg. `pa%das` search `pandas`.
- We can use `cmd s` to save clipboard history content as the snippet.
- When downloading collections of [Emojis workflow](http://joelcalifa.com/blog/alfred-emoji-snippet-pack/) unckeck strip option to keep all emojis text expansion options. e.g. :joy: will expand to joy symbol.

# Usage Tricks
1. Using action modifiers
  + For example type `github`, hit ctrl you will see fallback option, hit ctrl enter, it will google search github.
  
2. Use `bm` to search Safari and Chrome bookmarks.


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

# Useful Links
https://www.alfredapp.com/xmascalendar/
