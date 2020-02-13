#### How to extract file names and extensions?

```
filename=$(basename -- "$fullfile")
extension="${filename##*.}"
filename="${filename%.*}"
```
or
```
filename="${fullfile##*/}"
```
https://stackoverflow.com/questions/965053/extract-filename-and-extension-in-bash


#### How to exclude files on copying?

```
rsync -av --exclude='path1/to/exclude' --exclude='path2/to/exclude' source destination
```
https://askubuntu.com/questions/333640/cp-command-to-exclude-certain-files-from-being-copied


#### How to scrape a web page links?

`scrape.sh`

```
#!bin/bash

base="./resources/"
input=$base"urls.txt"
output=$base"temp.txt"
output2=$base"scraped_urls.txt"

`rm $output`

while IFS= read -r line
do
  `lynx -listonly -dump $line | awk '/http/{print $2}' | grep -e 'www.hogehoge.io' -e 'hogehoge.com' >> $output`
done < "$input"

# sort and uniq
`sort -n $output | uniq > $output2`
```

```
% sh ./scrape.sh
```
