# Problem: Macos can not verify some apps
Date: Oct 20, 2019

Error:
```
macOS cannot verify the developer of “_imaging.so”. Are you sure you want to open it?
```

Cause: Apple updated its securiy permissioins.

Solution:
```
- Find the relevant app, ctrl-click, and open in terminal.
- Once you opened the app, its verified automatically.
```

Example:
```
Alfred workflow: Alfred Image Utilities

- Selecte an image (a.jpg) in Finder
- double shift
- img (it fails, says `_imaging.so` is from unidentified source.

Go to Alfred workflow, and ctrl click and open the file in terminal.

Again, image conversion fails, this time,
`libjpeg.9.dylib` fails.

But I can not see this file in Alfred Workflow.
- Show all hidden files.
- Or, search for the file `find ~ -name "libjpeg.9.dylib"`

Its inside: `PIL/.dylibs/`
Make all these dynamic library files trusted as before.

Result: It worked.
```

