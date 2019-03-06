Script Filter code to create events workflow.

1. Find number of days remaining:
```python
from datetime import date
d = (date(2018,11,7)-date.today()).days
```

2. make list of dictionaries
```python
dict_list = [{k:v for k,v in zip(headers, list(zip(titles,subtitles,quicklookurls,days))[i])} 
              for i in range(len(titles))]
```

3.  sort dict by days
```python
sorted_dict_list = sorted(dict_list, key=lambda d: d['days'])
```

Full code:

```python
#!python
# -*- coding: utf-8 -*-#
import json
import sys
from datetime import date
import re

# We need to change FOUR things: title, days, subtitles and quicklookurls.

# INSERT SECOND ROW for title
# DO not forget COMMA in the end
titles = [
'Meetup Columbus Machine Learners',
'ISU Dinner at Baker',
'Homecoming Parade 2018',
'Dashain 2018']

# INSERT SECOND ROW for days
# DO not forget COMMA in the end
days = [
(date(2018,11,7)-date.today()).days,
(date(2018,11,11)-date.today()).days,
(date(2018,10,20)-date.today()).days,
(date(2018,10,19)-date.today()).days ]

# INSERT SECOND ROW for subtitle
# DO not forget COMMA in the end
subtitles = [ 
'(Nov 7 Wed,  7-9 pm)  Days: ',
'(Nov 11 Sun,  6-9 pm , Work 10-2pm)  Days: ',
'(Oct 20 Sat,  10 am)  Days: ',
'(Oct 19 Fri, 6 pm)  Days: ']

# INSERT SECOND ROW for quicklookurls
# DO not forget COMMA in the end
quicklookurls = [
'https://www.meetup.com/Columbus-Machine-Learners/events/skznxpyzcbdb/',
'https://www.facebook.com/events/408134099658615/',
'https://www.ohio.edu/alumni/newsletter-images/Homecoming/2018/1291-HomecomingShirts/1291-HomecomingShirts.html',
'']


#============================================================================================
# headers are fixed
headers = ['title','subtitle','quicklookurl','days']

# DO NOT MODIFY BELOW THIS!!!
# add days to subtitles
subtitles = [subtitles[i] + str(days[i]) for i in range(len(days))]

# make list of dictionaries
dict_list = [{k:v for k,v in zip(headers, list(zip(titles,subtitles,quicklookurls,days))[i])} for i in range(len(titles))]

# sort dict by days
sorted_dict_list = sorted(dict_list, key=lambda d: d['days'])

# without making negative days at end
#data = {"items": sorted_dict_list}
#json.dump(data, sys.stdout)

orig = sorted_dict_list
##===========================================================================
negs = []
for o in orig:
    num = int(re.compile(r'(-?\d+)$').search(o['subtitle']).group(1))
    if num < 0:
        orig.remove(o)
        negs.append(o)

dat_list = orig + negs
data = {"items": dat_list}
json.dump(data, sys.stdout)
```
