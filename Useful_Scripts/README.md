Table of Contents
=================
   * [Using External Trigger Example](#using-external-trigger-example)
   * [reading clipboard](#reading-clipboard)

# Using External Trigger Example
```
# A1: keyword object with name split imports

# A2: Run Script with bash command pbpaste

# A3: Run Script with python commands
import sys
import time
import os
import subprocess


APPLESCRIPT = """
tell application id "com.runningwithcrayons.Alfred" to run trigger "paste-and-down" in workflow "bhishan.test.paste" with argument "%s"
"""


def escape(s):
	"""Make string AppleScript safe."""
	return s.replace('"', '" & quote & "')


parts = sys.argv[1].split('\n#')


for i, s in enumerate(parts):
	s = s if i == 0 else '#' + s
	s = s.strip()
	if not s:
		continue

	# Call the External Trigger via AppleScript
	script = APPLESCRIPT % escape(s)
	subprocess.check_call(['/usr/bin/osascript', '-e', script])
	time.sleep(0.5)
#=====================================================================================================================
# B1: External with name paste-and-down
# B2: Copy to Clipboard with Automatically paste and Mark item transient.
# B3: delay 0.1 sec
# B4: Key Combo: Shift Enter

```

# reading clipboard
I can directly see the clipboard history using hot key ctrl-opt-c but sometimes, workflow is useful.
https://www.alfredforum.com/topic/13745-solved-json-config-so-confused/
```python
from contextlib import contextmanager
import os
import sqlite3

# Number of clipboard items to retrieve
COUNT = 10

# Path to clipboard history database
# For Alfred 3, replace "Alfred" with "Alfred 3"
dbpath = os.path.expanduser('~/Library/Application Support/Alfred/Databases/clipboard.alfdb')


@contextmanager
def database(path):
    """Open and close database."""
    db = sqlite3.connect(path)
    yield db
    db.close()

clips = []
with database(dbpath) as db:
    # each row is a tuple, even though we're only selecting one column
    rows = db.execute('SELECT item FROM clipboard ORDER BY ts DESC LIMIT ' + str(COUNT))
    clips = [row[0] for row in rows]

for s in clips:
    print(s)
```
