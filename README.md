# linux_cli
### AWK
== printer

awk options ’match {action }’ input-file > output-file
awk -F , '{print $2}' input-file

awk-F fs 
options == -F fs // seperate by whitespace 
: // seperate by :
, // seperate by ,
match == used for matching and regular expressions
{action} // Script == most commonly print + variable denominator
input-file == target file, stdin if omitted
output-file == save to target, stout if omitted

### sed
== Search and replace

https://www.baeldung.com/linux/remove-first-line-text-file#:~:text=sed%20is%20a%20common%20text,sed%20command%20is%20pretty%20straightforward.&text=The%20sed%20command%20in%20the,on%20line%20number%20%271%27.

sed options ’script ’ input-file > output-file
sed -e 's/"//g' input-file
sed -e ’s/"//g’ -e ’s/legit$/LEGIT/g’ input-file (WHY DOES THE LAST G NEED ONLY one /?)

sed scripts == -e 's/fun/sun/g'

options == -e // allows for scripting
'script' == substitution or /s fucntion most commmon
input-file == target file, stdin if omitted
output-file == target, stdout if omitted

### Grep

grep options pattern input-file(s) > output-file
grep -v legit input-file
grep -E "car|auto" task3mini.csv
grep -oE "car|auto" task3mini.csv

options == 
-i == ignore, case for matching
-E == treats pattern as an extended regular expression
-w == Match whole word
-o == print only the matched parts of a matching line, with each such part on a seperate output line
-v == inverts the match and prints lines that do not match the pattern

pattern == using this pattern, can be simple string or complex expressions like "^hello|bye$"
input-file == target file, stdin if omitted
output-file == target, stdout if omitted

### Niche Tool
wc == word count
-l == count lines
sort == sorts
-n == in numerical order
-r == reverse
uniq == removes duplicates from input
-c == add the count of duplicates
cut == removes columns (absolute postioning)

niche commands
#grab the first character in each line
$ head -5 task3mini.csv | cut -c1

Print from the 2nd character of a line onward
$ head -5 task3mini.csv | cut -c2-

### Printers
head == prints the 10 first
tail == prints the 10 last
cat == prints it all
echo == repeats echo input

1. How many lines does the file have? // wc -l legit-dga_domains.csv
3. What are the 6th to 16th characters of its its md5 checksum? // md5sum legit-dga_domains.csv | cut -c "6-16"
4. Clean up the file for further processing removing the header and the ” characters. save
the file as t3data.csv. // sed -e '1d' -e 's/"//g' legit-dga_domains.csv > t3data.csv
4. What is its md5 checksum now? // md5sum t3data.csv
5. How many different classes are used and how many entries in each class? // awk -F , '{print $3}' t3data.csv | sort | uniq -c
6. You notice some odd output from the above, due to some odd data. What is this data?
      2 
  52664 dga
      1 goz
  81261 legit
NOTE: One always needs to be wary of data that is not quite as clean as it seems.
7. How many subclases exist within the dga category and what are the number of records
labelled with these. // awk -F , '{if ($3 == "dga") print $4}' t3data.csv | sort | uniq -c
8. Taking the output above, print it as the category and then the count.  // awk -F , '{if ($3 == "dga") print $4}' t3data.csv | sort | uniq -cn
9. For the domains linked to cryptolocker, what are the top 5 (by count) of characters they
start with? // awk -F , '{if ($4 == "cryptolocker") print $2}' t3data.csv | sort | uniq -c
10. For the host linked to newgoz, what are the TLDs (the part after the final . in the name) 
that are used? Print them in ascending order of count. // awk -F , '{if ($4 == "newgoz") print $1}' t3data.csv | awk -F . '{print $NF}' | sort | uniq -c | sort -nr
11. Which country code or ccTLD ranks highest within the goz classified domains? // awk -F , '{if ($4 == "goz") print $1}' t3data.csv | awk -F . '{print $NF}' | sort | uniq -c | sort -nr

12. What line number/position is Iran in the listing above? Alternate question:
What line number/position is Iran for domains classified as legit?
13. As above, but print only the Statement as:
ir is in position x
14. (Advanced) Print out the two letter country codes from question 11 capitalised.
HINT: the tr command is useful for translating character mappings.

awk -F , '{if ($4 == "newgoz") print $1}' t3data.csv
