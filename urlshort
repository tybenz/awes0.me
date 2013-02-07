#!/bin/bash

echo "Generating URL..."

FULL_PATH="/Users/tbenzige/Projects/aws"
#Count is kept based on a list.txt file
#list.txt is a plain text file meant to show relationships between URLs
#Instead of a running count, we just count the lines in list.txt
INITIAL=`echo -n $(cat $FULL_PATH/list.txt | wc -l)`
NUM="$INITIAL/4"
NUM="$(($NUM*10000+10000))"
DICTIONARY=(a b c d e f g h i j k l m n o p q r s t u v w x y z A B C D E F G H I J K L M N O P Q R S T U V W X Y Z 0 1 2 3 4 5 6 7 8 9)

#Generate hash based on current URL count
if [ i = "0" ]; then
  echo "${DICTIONARY[0]}"
fi

DIR_NAME=""
base=66

while [ $NUM -gt 0 ]; do
  newchar="${DICTIONARY[$(($NUM%$base))]}"
  DIR_NAME="$DIR_NAME$newchar"
  NUM="$(($NUM/$base))"
done

#Create the directory and file corresponding to hash
#Append to list.txt for legibility and to keep track of total URL count
echo "Creating file..."
URL=$1
if echo "$URL" | grep "http://"; then
  URL=$1
else
  URL="http://$1"
fi
cd $FULL_PATH
N="
"
CONTENTS=`cat $FULL_PATH/list.txt`
FULL_URL="http://awes0.me/$DIR_NAME"
echo "$CONTENTS$N$N$n$FULL_URL$N|$N|------>$URL$N" > $FULL_PATH/list.txt

mkdir $FULL_PATH/$DIR_NAME &> /dev/null
echo "<script type=\"text/javascript\">window.location = '$URL'</script>" > $FULL_PATH/$DIR_NAME/index.html

#Copy into GitHub repo and push to gh-pages branch
echo "Uploading to GitHub..."
git add -A &> /dev/null
git commit -m "$URL added to shortener" &> /dev/null
git pull --rebase origin gh-pages &> /dev/null
git push origin gh-pages &> /dev/null
#Paste shortened URL into clipboard
echo "Putting shortened url in clipboard..."
echo -n "http://awes0.me/$DIR_NAME" | pbcopy &> /dev/null
echo
#Show contents of list.txt to reinforce relationship between long and short URLs
tail $FULL_PATH/list.txt
echo "Success!!"
