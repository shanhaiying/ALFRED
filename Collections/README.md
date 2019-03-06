Table of Contents
=================
   * [Important notes](#important-notes)
   * [Debugging Alfred](#debugging-alfred)
   * [Replace tabs by 4spaces](#replace-tabs-by-4spaces)
   * [Example of Script Filter](#example-of-script-filter)
   * [log or print current window of Finder](#log-or-print-current-window-of-finder)


# Important notes
> Disable or backup ALL the workflows that you have not used in last month.

```
To use github commit workflow, we need to enable javascript in safari.
  Safari > preferences > advanced > show develop menu in menubar
  Develop > Allow Javascripts from Apple Events
```


# Debugging Alfred
Example: In pisces computer:
```
$ /usr/bin/python --version
Python 3.5.2 -- Enthought, Inc. (x86_64)

Alfred wants python2.

Workflow: Powerthesaurus debugging
from: /usr/bin/python powerthesaurus.py "syn {query}"
to: /usr/local/bin/python2 powerthesaurus.py "syn {query}"
```

# Replace tabs by 4spaces
```python
import sys
import re


query = sys.argv[1]
lines = [s for s in query.split('\n')]
lines2 = [s.replace('\t','    ') for s in lines]

ans = '\n'.join(lines2)

sys.stdout.write(ans)
```

# Example of Script Filter
Connect this to Large Type in the end.
```python
import json
import sys

# headers
headers = ['title','quicklookurl','arg']
titles = list('abcde')
quicklookurls = ['']* len(titles)
args = titles

# make list of dictionaries
dict_list = [ {k:v for k,v in zip(headers, list(zip(titles,quicklookurls,args))[i]) } 
               for i in range(len(titles)) ]

# dump data
data = {"items": dict_list}
json.dump(data, sys.stdout)
```

# log or print current window of Finder
```applescript
tell application "Finder"
    if exists Finder window 1 then
        set currentDir to target of Finder window 1 as alias
    else
        set currentDir to desktop as alias
    end if
end tell
log POSIX path of currentDir
```

# Workflow simple timezones
```python
#===================================================================
# Name of timezones (You need to edit only these lines)
timezones = ["America/New_York","Asia/Kathmandu","America/Chicago","Europe/Brussels","Europe/Berlin","Europe/Madrid"]
cities = ['Athens', 'Kathmandu', 'Chicago', 'Hasselt', 'Frankfurt','Barcelona']
images = ['ou.png', 'nepal.png', 'chicago.jpeg', 'belgium.png', 'germany.png', 'spain.png']
titles = ['Athens (USA)', 'Kathmandu (Nepal)', 'Chicago (USA)', 'Hasselt (Belgium)', 'Frankfurt (Germany)', 'Barcelona (Spain)']


# Note: use timezones[i].split('/')[1] if you dont want separate cities names
#===================================================================
# Do not edit below this.
import sys
import json

from datetime import datetime
from pytz import timezone


# get cities from timezones
dat_list = []
fmt = '%Y %b %d, %I:%M %p'


cities_local_times = [datetime.now(timezone(tz)).strftime(fmt) for tz in timezones]
times = [i.split(',')[1] for i in cities_local_times]
for i in range(len(timezones)):
    dat_list.append({'title': titles[i] + times[i],
                     'subtitle': cities_local_times[i],
                     'icon': {'path': images[i]}
                    })



data = {"items": dat_list}
json.dump(data, sys.stdout)

# NOTE: to get list of time zones
# https://en.wikipedia.org/wiki/List_of_tz_database_time_zones
#
#for tz in pytz.all_timezones:
#    print (tz)
```

# Workflow events using Script Filter
```python
import json
import sys
from datetime import date
import re

'''
#example event:

Tihar Bhai Tika 2075 @ North Carolina
date(2018,11,9)-date.today()).days
'(Nov 9 Fri, North Carolina)  Days: '

'''

# data
data_lst = [
    # first event
    ['DE School 2019 @ Berkeley',
     (date(2019,2,25)-date.today()).days,
     '(Feb 25 Mon - Mar 1 Fri, UC Berkeley )  Days: ',
    ],
    # another event
    ['Last day of year @ 2019',
     (date(2019,12,31)-date.today()).days,
     '(Dec 31 Tue, Last day of year 2019)  Days: '
    ]
]

#========================================================================
# DO NOT MODIFY BELOW THIS!!!

titles    = [i[0] for i in data_lst]
days      = [i[1] for i in data_lst]
subtitles = [i[2] for i in data_lst]

# headers are fixed
headers = ['title','subtitle','days']

# add days to subtitles
subtitles = [subtitles[i] + str(days[i]) for i in range(len(days))]

# make list of dictionaries
dict_list = [{k:v for k,v in zip(headers, list(zip(titles,subtitles,days))[i]) } for i in range(len(titles)) if days[i]>=0 ]

# sort dict by days
sorted_dict_list = sorted(dict_list, key=lambda d: d['days'])

data = {"items": sorted_dict_list}
json.dump(data, sys.stdout)
```
