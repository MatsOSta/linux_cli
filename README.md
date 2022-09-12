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
