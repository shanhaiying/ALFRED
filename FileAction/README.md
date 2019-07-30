Table of Contents
=================
   * [compress pdf using ghostscript](#compress-pdf-using-ghostscript)
   * [compress pdf using ps2pdf](#compress-pdf-using-ps2pdf)
   * [compress pdf using ColorSync Utility](#compress-pdf-using-colorsync-utility)
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

# compress pdf using ps2pdf
```bash
man ps2pdf # ps2pdf uses arguments same of ghostscript
/usr/local/bin/ps2pdf -dPDFSETTINGS=/ebook input.pdf outptu.pdf
```

# compress pdf using ColorSync Utility
```
1. First create custom filter, choose 50% size and quality medium.
2. Then open pdf in colorsync, file > use quartz to reduce size
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
