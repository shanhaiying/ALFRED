Table of Contents
=================
   * [compress pdf using ghostscript](#compress-pdf-using-ghostscript)
   * [convert multiple png to pdf using imagemagic command convert](#convert-multiple-png-to-pdf-using-imagemagic-command-convert)

# compress pdf using ghostscript
```bash
# input file
IN="$1"
BASEE=$(basename "$IN")
DIR=$(dirname "$IN")
OUT="$DIR"/small_"$BASEE"

# compress using ebook format of ghostscript
/usr/local/bin/gs -sDEVICE=pdfwrite -dNOPAUSE -dQUIET -dBATCH -dPDFSETTINGS=/ebook -dCompatibilityLevel=1.4 -sOutputFile="$OUT" "$1"
```

# convert multiple png to pdf using imagemagic command convert
```bash
# Split tab-delimited query into an array
query="{query}"
oIFS="$IFS"
IFS=$'\t' args=( $query )
IFS="$oIFS"

# echo
# echo "${args[@]}"

PNG="$args"
DIR=$(dirname "$PNG")
OUT="$DIR"/combined.pdf

#echo -n "$OUT" > out.txt


# combine pngs to pdf using imagemagic command convert
/usr/local/bin/convert "${args[@]}" "$OUT"

# make the pdf small
IN="$OUT"
BASEE=$(basename "$IN")
DIR=$(dirname "$IN")
OUT="$DIR"/small_"$BASEE"

/usr/local/bin/gs -sDEVICE=pdfwrite -dNOPAUSE -dQUIET -dBATCH -dPDFSETTINGS=/ebook -dCompatibilityLevel=1.4 -sOutputFile="$OUT" "$IN"
```
