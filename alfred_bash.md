# Working with multiple file selection
```bash
# Change IFS to TAB and expand into an array
IFS=$'\t' filesListArr=($@)

# Loop over the file list array
for file in "${filesListArr[@]}"
do
    trimmedPath="$(echo -e "${file}" | xargs)"
    # Your script to be run
    mv -i "$trimmedPath" ~/Downloads
done
```
