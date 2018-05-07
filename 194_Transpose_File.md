# Transpose File
## Description
Given a text file file.txt, transpose its content.

You may assume that each row has the same number of columns and each field is separated by the ' ' character.

Example:

If file.txt has the following content:
```
name age
alice 21
ryan 30
```
Output the following:
```
name alice ryan
age 21 30
```
## Solution
```bash
# Read from the file file.txt and print its transposed content to stdout.
array=()
while read -a columns; do
    for(( i = 0; i < ${#columns[@]}; i++ )); do
        array[i]="${array[i]} ${columns[i]}"
    done
done < file.txt

for(( i = 0; i < ${#array[@]}; i++)); do
    echo ${array[i]}
done
```
