# Quickview snippets
```bash
# Run Script
pbpaste > a.py
echo a.py

# Write Text File
Filename: ~/Dropbox/Alfred.alfredpreferences/workflows/user.workflow.AD6DFBD4-D577-4B5F-8367-25FD446EA71A/a.tex

\documentclass{article}
\usepackage{minted}
\begin{document}
\begin{minted}{python}
{clipboard}
\end{minted}
\end{document}

# Terminal Command
cd ~/Dropbox/Alfred.alfredpreferences/workflows/user.workflow.AD6DFBD4-D577-4B5F-8367-25FD446EA71A
pdflatex -shell-escape a.tex && osascript -e 'tell application "Terminal" to set visible of front window to false' && qlmanage -p a.pdf && exit

# NOTES: 
# 1. Running bash scripts on alfred fails to run pdflatex command or /Library/TeX/texbin/pdflatex command.
# 2. converted pdf trims long lines in that case simply view a.py instead of a.pdf using asnip command.
# 3. python package code2pdf needs pyqt4 and installing it gives problem and is a heavy program
# 4. pandoc mycode.py -o mycode.pdf gives wrong outputs, does not recognize new lines
```
