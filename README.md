Table of Contents
=================
   * [Currently Useful Shortcuts](#currently-useful-shortcuts)
   * [My useful workflows](#my-useful-workflows)
   * [Useful Applescripts](#useful-applescripts)
   * [Alfred arguments bash and python](#alfred-arguments-bash-and-python)
   * [Alfred Settings](#alfred-settings)
   * [Alfred Tips](#alfred-tips)
   * [Workflow python2 and python3](#workflow-python2-and-python3)
   * [Run python script](#run-python-script)
   * [Scatterplot using plotly](#scatterplot-using-plotly)

# Currently Useful Shortcuts
```
NOTE: Please regularly disable unused workflows and unused key mappings.
- (May be copy something form cmd cmd to clipboard) Then, qq or qq sh  # quick view of clipboard in fenetre.
  Then alt shift o (default keymap from Fenetre) to open all opened files in Fentre.
  (Click eye button in Fentere instead of Close button. Alt H to hide window.)
- cpd or cpda  # copy latest downloads to PWD or copy all downloads to PWD
- Alt cmd c  ==> copy content of selected file to clipboard.
- opsh ==> open dropbox shared folder.
- hely, helps, helt ==> Open website youtube, pandas, tedTalk, in Helium.
- pdf hello ==> search hello.pdf file.
- bswitch ==> toggle current url in safari and chrome
- cmd shift d ==> duplicate line (aa text manipulation)
   cmd shift ] ==> indent
- Jupyter notebook
  cmd sh enter ==> make clipboard markdown and enter
  alt sh enter ==> make clipbpard markdown header and enter
- Leetcode
  copy the python class from leetcode
  leet keyword will reformat the class and paste in visual studio code.
```

# My useful workflows
- `gh alfred` to visit this github Alfred repository.
- Copy something or copy from clipboard viewer. Hit `qq` or `qq sh (for shell)` then we can see copied text in Fenetre app where we can see syntax highlight and also copy file contents.
- [last2imgur](https://github.com/aviaryan/alfred-last2imgur) upload last screenshot to imgur. 
  This workflow does not require any other dependencies. We just need to edit the default path of screenshot in getfile.sh.
  
# Useful Applescripts
Calling Alfred from itself. First create a `input > keyword`. Then use this applescript. Then use key combo `cmd shift left` to select current line leftwards. Then use keycombo `cmd c` to copy it. Then do whatever you like with the copied text.
```applescript
tell application "Alfred 4" to search "{query}"
```

Another example:
```applescript
-- Path of currently selected file in Finder
	tell application "Finder"
		set someSource to selection as alias list
		if someSource = {} then
			return "Select a file in Finder first"
		end if
		set theFile to item 1 of someSource as alias
        return POSIX path of theFile
	end tell
```

# Alfred arguments bash and python
https://www.alfredforum.com/topic/9070-how-to-workflowenvironment-variables/

Using args in Bash
```bash
# using built-in split
We can not use space as separator (can use comma, colon etc) and gives split1 split2 split3 etc.
But I like to separate arguments by space, as that is the most natural way of doing it.

# split the arguments
fN=`echo $1 | cut -d' ' -f1`
x=`echo $1 | cut -d' ' -f2`
y=`echo $1 | cut -d' ' -f3`

# split the argument variable called c0_c1
c0=`echo "$c0_c1" | cut -d' ' -f1`
c1=`echo "$c0_c1" | cut -d' ' -f2`

# using array does not work in pisces
#args=( $my_args_name )
#split0="${args[0]}"
#split1="${args[1]}"
```

Using arguments in Python
```python
import os
args = os.environ['my_args_name']
args = os.getenv('my_args_name')

then,
arg0, arg1 = args.split(' ')
```


# Alfred Settings
- Web Bookmarks:  show bookmarks via keyword bm  (works for chrome and safari)
- Calculator : Enable advanced calulator and standard calculator.
- Clipboard double alt, snippet double cmd, Alfred Hotkey double shift.

For brand new Alfred use following settings:
```
Note: Web searches are deleted if we upgrade Alfred3 to Alfred 4, but workflows are kept intact.

1. alfred hot key: General >  shift shift

2. Features > Clipboard History 
   hotkey: cmd cmd  (mnemonic c means clipboard)
   check: keep plain text 3 month, images 24 hr, file 24 hr
   uncheck: snippets, simply use clipboards not snippets
   merging: use fast append and place merged back to macos
           (copy line1, select line2 hold cmd hit cc, then paste)
   
3. Features > Snippets > alt alt
   check Automatically expand snippets by keyword.
   click Auto Expansion Options below it and then turn off sound.
   type ?snip in alfred to open snippet window
   type snip hello to search snippet hello in alfred.
   
4. Features > Actions  keep it default opt cmd \  to do file action
   Go to File Actions and unckech unwanted file actions.
   Go to finder, select a file, hit opt cmd \, this will take to file action in Alfred.
   
5. Features > Web Bookmarks
   check safari and chrome bookmarks
   There is no bm keyword for bookmark in Alfred4, simply type bookmared website name, it will show it.
   
 6. Features > Calculator
    Enable standard calculator
    
 7. Features > iTunes
    Disable hotkey and keywords, I don't use iTunes.
```


# Alfred Tips
[Alfred Cheatsheet](https://www.alfredapp.com/help/getting-started/cheatsheet/).  

- We can use SQL like string search in Clipboard search: eg. `pa%das` search `pandas`.

- First copy some contents, hit `alt alt` to view clipboard history, hit `cmd s` to save as the snippet.

- When downloading collections of [Emojis workflow](http://joelcalifa.com/blog/alfred-emoji-snippet-pack/) unckeck strip option to keep all emojis text expansion options. e.g. :joy: will expand to joy symbol.

- `Alfred > Clipboard > Merging > Select Fast append selected text`. Then copy something, select another text and hit `cmd c c`, it will be appended to previous copy and can be pasted as a whole.

- Open URL supports {query}. Example: Use `http://www.google.com/search?q={query}&btnI` for google lucky query.

-  Using action modifiers
  + For example type `github`, hit ctrl you will see fallback option, hit ctrl enter, it will google search github.
  
- Use `bm` to search Safari and Chrome bookmarks.


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

# Run python script
```bash
# split the args variable
c0=`echo "$c0_c1" | cut -d' ' -f1`
c1=`echo "$c0_c1" | cut -d' ' -f2`

# run the python script
if [ -f "/Users/poudel/miniconda3/envs/dataSc/bin/python" ]
then
  /Users/poudel/miniconda3/envs/dataSc/bin/python scatterplot.py "$1" "${c0-0}" "${c1-1}"
else
  /Users/poudel/Library/Enthought/Canopy/edm/envs/User/bin/python scatterplot.py "$1" "${c0-0}" "${c1-1}"
fi
```

# Scatterplot using plotly
```python
# File: plotly_scatterplot.py
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import sys


import plotly.offline as py
import plotly.graph_objs as go

def get_header_sep(infile):
    header = None
    sep = r'\s+'
    names = None
    with open(infile) as fo:
        for line in fo:
            # when first row is commented
            #   #a,b,c   or #1,2,3
            if line.startswith('#'):
                header = None
                if ',' in line:
                    names = line.lstrip('#').split(',')
                    names = [i.strip() for i in names]
                    sep = ','
                else:
                    names = line.lstrip('#').split()
                    sep = ' '
            
            # when first row is not commented
            #    a,b,c  or 1,2,3
            else:
                if ',' in line:
                    sep = ','
                else:
                    sep = ' '
                

                parts = line.strip().split(sep)
                # when first row is   1.0,2.0,3.0
                if parts[0].replace('.','').isnumeric():
                    header = None
                    names = None
                else:
                    # when first row is   a,b,c
                    header = 0
                    names = None
            break
    return header, sep, names

def plotly_scatterplot(infile, cols, header, sep, names):
    df = pd.read_csv(infile,header=header,sep=sep,
                     comment='#',names=names,engine='python')
    
    # make columns strings or digits

    cols = [ int(col) if str(cols[0]).isdigit() else str(col) for col in cols ]
    c0, c1 = cols

    # x and y axis names
    x_col = df.columns[int(c0)] if str(c0).isdigit() else c0
    y_col = df.columns[int(c1)] if str(c1).isdigit() else c1

    sc1 = go.Scatter(x=df[x_col],
                     y=df[y_col],
                     mode = 'markers',
                     #text = [str(i)+','+str(j) for i,j in zip(df[x_col].values,df[y_col].values)],
                     name = 'plot1')

    mydata= [sc1]
    layout = go.Layout(
                    title=' ',
                    xaxis=dict(
                               title=x_col,
                               titlefont=dict(
                               family='Courier New, monospace',
                               size=18,
                               color='#7f7f7f')),
                     yaxis=dict(title=y_col,
                                titlefont=dict(
                                          family='Courier New, monospace',
                                          size=18,
                                          color='#7f7f7f')))
    
    myfig = go.Figure(data=mydata, layout=layout)

    # iplot plots in jupyter-notebook, plot opens in new tab.
    return py.plot(myfig, filename='myplot.html')

# plot      
infile = sys.argv[1].strip()
cols = [0,1 ]
if sys.argv[2]:
    cols = sys.argv[2].split(' ')

# read data
header, sep, names = get_header_sep(infile)

if not sep.strip() == ',':
    sep = r'\s+'
    
plotly_scatterplot(infile, cols, header, sep, names)
```
