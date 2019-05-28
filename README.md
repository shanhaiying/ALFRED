Table of Contents
=================
   * [Currently Useful Shortcuts](#currently-useful-shortcuts)
   * [Alfred Settings](#alfred-settings)
   * [Alfred Tips](#alfred-tips)
   * [My useful workflows](#my-useful-workflows)
   * [Usage Tricks](#usage-tricks)
   * [Workflow python2 and python3](#workflow-python2-and-python3)
   * [Snippet working for substring](#snippet-working-for-substring)
   * [Replace substring from copied text](#replace-substring-from-copied-text)
   * [Useful Links](#useful-links)
   
# Currently Useful Shortcuts
```
1. qq or qq sh  # quick view of clipboard in fenetre.
2. Alt cmd c  ==> copy content of selected file to clipboard.
3. opsh ==> open dropbox shared folder.
4. hely, helps, helt ==> Open website youtube, pandas, tedTalk, in Helium.
5. pdf hello ==> search hello.pdf file.
6. bswitch ==> toggle current url in safari and chrome
```

# Alfred Settings
- Web Bookmarks:  show bookmarks via keyword bm  (works for chrome and safari)
- Calculator : Enable advanced calulator and standard calculator.
- Clipboard double alt, snippet double cmd, Alfred Hotkey double shift.

# Alfred Tips
[Alfred Cheatsheet](https://www.alfredapp.com/help/getting-started/cheatsheet/).  
- We can use SQL like string search in Clipboard search: eg. `pa%das` search `pandas`.
- First copy some contents, hit `alt alt` to view clipboard history, hit `cmd s` to save as the snippet.
- When downloading collections of [Emojis workflow](http://joelcalifa.com/blog/alfred-emoji-snippet-pack/) unckeck strip option to keep all emojis text expansion options. e.g. :joy: will expand to joy symbol.
- `Alfred > Clipboard > Merging > Select Fast append selected text`. Then copy something, select another text and hit `cmd c c`, it will be appended to previous copy and can be pasted as a whole.

# My useful workflows
- Copy something or copy from clipboard viewer. Hit `qq` or `qq sh (for shell)` then we can see copied text in Fenetre app where we can see syntax highlight and also copy file contents.

# Usage Tricks
1. Using action modifiers
  + For example type `github`, hit ctrl you will see fallback option, hit ctrl enter, it will google search github.
  
2. Use `bm` to search Safari and Chrome bookmarks.

# Workflow python2 and python3
Most of Alfred workflows are in python2. For exmple "adsinspire", "arxiv" research workflows does not work with python3.
To fix this we can set up python as python2.  
Some errors:
```
1. cPickle not found.
2. .decode('utf-8') does work.
3. There are so many places to edit the fixes.
4. Also, fixum workflow does not work in python3.
```
```bash
/usr/bin/python --version # Python 3.5.2 -- Enthought, Inc. (x86_64)
sudo mv /usr/bin/python /usr/bin/python36 # create backup

which python2 # /usr/local/bin/python2
sudo ln -s /usr/local/bin/python2 /usr/bin/python

/usr/bin/python --version # Python 2.7.14
# Now Workflow will work.
```

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
