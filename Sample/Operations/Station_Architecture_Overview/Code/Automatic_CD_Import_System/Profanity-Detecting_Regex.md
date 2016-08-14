A file of regular expressions to detect profanity and their various misspellings and variations.

[This file](https://wiki.wmfo.org/@api/deki/files/53/=filter.txt "filter.txt") is meant to be run with case-insensitive search.  It will only detect lower-case profanity otherwise.  The hash (\#) is treated as a comment character; any line beginning with a '\#' contains no regular expression, and instead contains a comment for the user.

The format of the file is printed here, and is also explained at the top of the file in comments.

**Format:**

\# Original word: 'X'

\# Spelling variations of 'X' in regex; commented out because they're covered by the last line (e.g. covers fuk and pussi)

Vowel-to-nonalphabetic-character substitutions or vowel omissions (e.g. covers f\*ck and pssy)

Inner letter-to-nonalphabetic substitutions (e.g. cover f\*\*k or p\*\*\*y)

Cover the original spelling variations, and randomly inserted or repeated characters (e.g. fuk, fuck, fuuuuck, fu--c032k)

*
[Page Attachments](https://wiki-files.wmfo.org/Operations/Station_Architecture_Overview/Code/Automatic_CD_Import_System/Profanity-Detecting_Regex)
