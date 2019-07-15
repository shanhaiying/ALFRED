# remove empty lines and put - at the beginning
```
Before:
list1

list2

After:
- list1
- list2

Method:
- select all text, cut it
- delemp  # workflow to delete empty lines
- fr (.*) -\s\1  # find and replace whole line by - and whole line
```
