# nginx-regx
nginx regx config
--------------------------------------------------------------------------------------------------------------------------------------------
 Search-Order       Modifier       Description                                                        Match-Type        Stops-search-on-match
--------------------------------------------------------------------------------------------------------------------------------------------
     1st               =           The URI must match the specified pattern exactly                  Simple-string              Yes
     2nd               ^~          The URI must begin with the specified pattern                     Simple-string              Yes
     3rd             (None)        The URI must begin with the specified pattern                     Simple-string               No
     4th               ~           The URI must be a case-sensitive match to the specified Rx      Perl-Compatible-Rx      Yes (first match)                 
     4th               ~*          The URI must be a case-insensitive match to the specified Rx    Perl-Compatible-Rx      Yes (first match)
     N/A               @           Defines a named location block.                                   Simple-string              Yes
 --------------------------------------------------------------------------------------------------------------------------------------------

 -----------------------------------------------------------------------------------------
    ()    : Group/Capturing-group, capturing mean match and retain/output/use what matched
            the patern inside (). the default bracket mode is "capturing group" while (?:) 
            is a non capturing group. example (?:a|b) match a or b in a non capturing mode
 ----------------------------------------------------------------------------------------- 
    ?:    : Non capturing group
    ?=    : Positive look ahead 
    ?!    : is for negative look ahead (do not match the following...)
    ?<=   : is for positive look behind
    ?<!   : is for negative look behind
 -----------------------------------------------------------------------------------------

 -----------------------------------------------------------------------------------------
     /    : It doesn't actually do anything. In Javascript, Perl and some other languages, 
            it is used as a delimiter character explicitly for regular expressions.
            Some languages like PHP use it as a delimiter inside a string, 
            with additional options passed at the end, just like Javascript and Perl.
            Nginx does not use delimiter, / can be escaped with \/ for code portability 
            purpose BUT this is not required for nginx / are handled literally 
            (don't have other meaning than /)
 -----------------------------------------------------------------------------------------

 -----------------------------------------------------------------------------------------
     ~     : Enable regex mode for location (in regex ~ mean case-sensitive match)
     ~*    : case-insensitive match
     |     : Or
     ()    : Match group or evaluate the content of ()
     $     : the expression must be at the end of the evaluated text 
             (no char/text after the match) $ is usually used at the end of a regex 
             location expression. 
     ?     : Check for zero or one occurrence of the previous char ex jpe?g
     ^~    : The match must be at the beginning of the text, note that nginx will not perform 
             any further regular expression match even if an other match is available 
             (check the table above); ^ indicate that the match must be at the start of 
             the uri text, while ~ indicates a regular expression match mode.
             example (location ^~ /realestate/.*)
             Nginx evaluation exactly this as don't check regexp locations if this 
             location is longest prefix match.
     =     : Exact match, no sub folders (location = /)
     ^     : Match the beginning of the text (opposite of $). By itself, ^ is a 
             shortcut for all paths (since they all have a beginning).
     .*    : Match zero, one or more occurrence of any char
     \     : Escape the next char
     .     : Any char 
     *     : Match zero, one or more occurrence of the previous char
     !     : Not (negative look ahead)
     {}    : Match a specific number of occurrence ex. [0-9]{3} match 342 but not 32
             {2,4} match length of 2, 3 and 4
     +     : Match one or more occurrence of the previous char 
     []    : Match any char inside
 --------------------------------------------------------------------------------------------
### ref

Any character except [\^$.|?*+()	Literal character

\ followed by any of [\^$.|?*+(){}	Backslash escapes a metacharacter

.	Any character

|	Alternation

\|	Alternation

?	Greedy quantifier

\?	Greedy quantifier

??	Lazy quantifier

?+	Possessive quantifier

*	Greedy quantifier
*	
*?	Lazy quantifier

*+	Possessive quantifier

+	Greedy quantifier
+	
\+	Greedy quantifier

+?	Lazy quantifier

++	Possessive quantifier

{ and }	Literal curly braces

{n} where n is an integer >= 1	Fixed quantifier

{n,m} where n >= 0 and m >= n	Greedy quantifier

{n,} where n >= 0	Greedy quantifier

{,m} where m >= 1	Greedy quantifier

\{n\} where n is an integer >= 1	Fixed quantifier

\{n,m\} where n >= 0 and m >= n	Greedy quantifier

\{n,\} where n >= 0	Greedy quantifier

\{,m\} where m >= 1	Greedy quantifier

{n,m}? where n >= 0 and m >= n	Lazy quantifier

{n,}? where n >= 0	Lazy quantifier

{,m}? where m >= 1	Lazy quantifier

{n,m}+ where n >= 0 and m >= n	Possessive quantifier

{n,}+ where n >= 0	Possessive quantifier

^	String anchor

^	Line anchor

$	String anchor

$	Line anchor

\a	Character escape

\A	String anchor

\A	Attempt anchor

\b	Word boundary

\b	Backspace character

\B	Word non-boundary

\B	Backslash character

\c	XML shorthand

\ca through \cz	Control character escape

\cA through \cZ	Control character escape

\C	XML shorthand

\d	Digits shorthand

\D	Non-digits shorthand

\e	Escape character

\f	Form feed character

\g{name}	Named backreference

\g-1, \g-2, etc.	Relative Backreference

\g{-1}, \g{-2}, etc.	Relative Backreference

\g1 through \g99	Backreference

\g{1} through \g{99}	Backreference

\g<name> where “name” is the name of a capturing group	Named subroutine call
 
\g<name> where “name” is the name of a capturing group	Named backreference
 
\g'name' where “name” is the name of a capturing group	Named subroutine call
 
\g'name' where “name” is the name of a capturing group	Named backreference
 
\g<0>	Recursion
 
\g'0'	Recursion

\g<1> where 1 is the number of a capturing group	Subroutine call
 
\g<1> where 1 is the number of a capturing group	Backreference
 
\g'1' where 1 is the number of a capturing group	Subroutine call
 
\g'1' where 1 is the number of a capturing group	Backreference
 
\g<-1> where -1 is a negative integer	Relative subroutine call
 
\g<-1> where -1 is a negative integer	Relative backreference
 
\g'-1' where -1 is a negative integer	Relative subroutine call
 
\g'-1' where -1 is a negative integer	Relative backreference
 
\g<+1> where +1 is a positive integer	Forward subroutine call
 
\g'+1' where +1 is a positive integer	Forward subroutine call
 
\G	Attempt anchor
 
\G	Match anchor
 
\h	Hexadecimal digit shorthand
 
\h	Horizontal whitespace shorthand
 
\H	Non-hexadecimal digit shorthand
 
\H	Non-horizontal whitespace shorthand
 
\i	XML shorthand
 
\I	XML shorthand
 
\k<name>	Named backreference
 
\k'name' through \k'99'	Named backreference
 
\k{name}	Named backreference
 
\k<1> through \k<99>	Backreference
 
\k'1' through \k'99'	Backreference
 
\k<-1>, \k<-2>, etc.	Relative Backreference
 
\k'-1', \k'-2', etc.	Relative Backreference
 
\K	Keep text out of the regex match
 
\l	Lowercase shorthand
 
\L	Non-lowercase shorthand
 
\m	Tcl start of word boundary
 
\M	Tcl end of word boundary
 
\n	Line feed character
 
\N	Not a line break
 
Literal CRLF, LF, or CR line break	Line break
 
\o{7777} where 7777 is any octal number	Octal escape
 
\pL where L is a Unicode category	Unicode category
 
\PL where L is a Unicode category	Unicode category
 
\p{L} where L is a Unicode category	Unicode category
 
\p{IsL} where L is a Unicode category	Unicode category
 
\p{Category}	Unicode category
 
\p{IsCategory}	Unicode category
 
\p{Script}	Unicode script
 
\p{IsScript}	Unicode script
 
\p{Block}	Unicode block
 
\p{InBlock}	Unicode block
 
\p{IsBlock}	Unicode block
 
\P{Property}	Negated Unicode property
 
\p{^Property}	Negated Unicode property
 
\P{^Property}	Unicode property
 
\Q…\E	Escape sequence
 
\r	Carriage return character
 
\R	Line break
 
\s	Whitespace shorthand
 
\S	Non-whitespace shorthand
 
\t	Tab character
 
\u	Uppercase shorthand
 
\uFFFF where FFFF are 4 hexadecimal digits	Unicode code point
 
\u{FFFF} where FFFF are 1 to 4 hexadecimal digits	Unicode code point
 
\U	Non-uppercase shorthand
 
\v	Vertical tab character
 
\v	Vertical whitespace shorthand
 
\V	Non-vertical whitespace shorthand
 
\w	Word character shorthand
 
\W	Non-word character shorthand
 
\xFF where FF are 2 hexadecimal digits	Hexadecimal escape
 
\xFFFF where FFFF are 4 hexadecimal digits	Unicode code point
 
\x{FFFF} where FFFF are 1 to 4 hexadecimal digits	Unicode code point
 
\X	Unicode grapheme
 
\y	Tcl word boundary
 
\Y	Tcl word non-boundary
 
\Z	String anchor
 
\z	String anchor
 
\0	NULL escape
 
\1 through \7	Octal escape
 
\1 through \9	Backreference
 
\10 through \77	Octal escape
 
\10 through \99	Backreference
 
\100 through \377	Octal escape
 
\01 through \0377	Octal escape
 
\‘	String anchor
 
\‘	Attempt anchor
 
\'	String anchor
 
\<	GNU word boundary
      
\>	GNU word boundary
 
[[:<:]]	POSIX word boundary
        
[[:>:]]	POSIX word boundary
 
(regex)	Capturing group
 
\(regex\)	Capturing group
 
(?:regex)	Non-capturing group
 
(?<name>regex)	Named capturing group
 
(?'name'regex)	Named capturing group
 
(?#comment)	Comment
 
(?|regex)	Branch reset group
 
(?>regex)	Atomic group
 
(?=regex)	Positive lookahead
 
(?!regex)	Negative lookahead
 
(?<=regex)	Positive lookbehind
          
(?<!regex)	Negative lookbehind
 
(?(?=regex)then|else) where (?=regex) is any valid lookaround and then and else are any valid regexes	Lookaround conditional
 
(?(regex)then|else) where regex, then, and else are any valid regexes and regex is not the name of a capturing group	Implicit lookahead conditional
 
(?(name)then|else) where name is the name of a capturing group and then and else are any valid regexes	Named conditional
 
(?(<name>)then|else) where name is the name of a capturing group and then and else are any valid regexes	Named conditional
 
(?('name')then|else) where name is the name of a capturing group and then and else are any valid regexes	Named conditional
 
(?(1)then|else) where 1 is the number of a capturing group and then and else are any valid regexes	Conditional
 
(?(-1)then|else) where -1 is a negative integer and then and else are any valid regexes	Relative conditional
 
(?(+1)then|else) where +1 is a positive integer and then and else are any valid regexes	Forward conditional
 
(?(+1)then|else) where 1 is the number of a capturing group and then and else are any valid regexes	Conditional
 
(?<capture-subtract>regex) where “capture” and “subtract” are group names and “regex” is any regex	Balancing group
 
(?'capture-subtract'regex) where “capture” and “subtract” are group names and “regex” is any regex	Balancing group
 
(?&name) where “name” is the name of a capturing group	Named subroutine call
 
(?(DEFINE)regex) where “regex” is any regex	Subroutine definitions
 
(?P<name>regex)	Named capturing group
 
(?P=name)	Named backreference
 
(?P=1) through (?P=99)	Backreference
 
(?P>name) where “name” is the name of a capturing group	Named subroutine call
 
(?R)	Recursion
 
(?0)	Recursion
 
(?1) where 1 is the number of a capturing group	Subroutine call
 
(?-1) where -1 is a negative integer	Relative subroutine call
 
(?+1) where +1 is a positive integer	Forward subroutine call
 

Character Class Syntax	Feature
 
Any character except ^-]\	Literal character
 
\ (backslash) followed by any of ^-]\	Backslash escapes a metacharacter
 
\	Literal backslash
 
- between two tokens that each specify a single character	Range
 
^ immediately after the opening [	Negated character class
 
[	Literal opening bracket
 
[	Nested character class
 
[base-[subtract]]	Character class subtraction
 
[base&&[intersect]]	Character class intersection
 
[base&&intersect]	Character class intersection
 
[:alpha:]	POSIX class
 
[:^alpha:]	Negated POSIX class
 
\p{Alpha}	POSIX class
 
\p{IsAlpha}	POSIX class
 
[.span-ll.]	POSIX collation sequence
 
[=x=]	POSIX character equivalence


