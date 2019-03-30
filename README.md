# ALFRED
My Alfred workflows and publications

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
