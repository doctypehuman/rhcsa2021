# Grep and Regular Expression


1. [Grep](##Grep)

2. [Regular Expression](##Regular-Expression)




## Grep

Grep is a command which allows us to filter relevant data from a file(s).

Usage: grep \[options\] "string/pattern" file1 file2 file3 OR cat file |  grep \[options\] "string/pattern" 

Options:

- -i Case insensitive

- -w Matches whole word

- -o Print or display only matched word

- -n Prints line number along with the result

- -c Prints matched number of lines

- -A Prints _n_ number of lines after the match. \(grep -A 3 string file \)

- -B Prints _n_ number of lines before the match.

- -C Prints _n_ number of lines around the match.

- -r Recursive search 

- -l Display only file names

- -h Hides file names

- -f Takes search string/pattern from a file. One per line.

- -e Search multiple strings 

- -E To work with patterns

The power of grep can be further multiplied by using the *cut* command with it.


## Regular Expression 

There are certain characters in Linux which have special meanings. They can be used to create a pattern which is then supplied to a command like Grep as an argument. 

I am listing the basics that I know of and those that can be used to create a pattern for Grep. 


- xy|ab : Searches for either xy or ab

- ^xyz  : Searches for lines which begin with xyz

- xyz$  : Searches for lines ending with xyz

- ^$    : Searches for empty lines

-  \    : Removes the meaning of a special character \( \^ \) This will search for the ^ sign rather than search for at the begining of the line.

-  .    : Matches any one character

- \\.   : Matches for exactly with .

- \b	 : Matches the empty string at the edge of the word

- ?     : Preceding character is optional and will be matched once

- \[xyz\] : Matches for x , y or z

- \[a-d\] : Is equal to a,b,c,d 

- \[a-ds-z\] : Is equal to abcdstuvwxyz

- \\^\[abc\] : Matches for lines begining with a or b or c

- \{N\} : The preceeding string is matched exactly N times

- \{N,\} : The preceeding string is matched N or more times

- \{N,M\} : The preceeding string is matched N times but not more than M times

- \[\[:alnum:\]\] : Matches alphanumeric characters

- \[\[:alpha:\]\] : Matches alphabets

- \[\[:blank:\]\] : Matches blanck characters, spaces , tabs

- \[\[:digit:\]\] : Matches digits \(0-9\)

- \[\[:lower:\]\] : Matches lowercase alphabets 

- \[\[:upper:\]\] : Matches uppercase alphabets

- \[\[:space:\]\] : Matches space characters like carriage return, tab, newline, vertical tab

