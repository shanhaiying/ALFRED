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
