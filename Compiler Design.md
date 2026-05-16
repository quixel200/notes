



# Lexical Analysis

identify valid words

different types of formatting possible(tab vs spaces)

## role:
lexical analyser -> token -> parser -> semantic analysis
(both use symbol table)


## tokens, patterns and lexemes
a token is a pair
name: token value(option)

a  pattern is a descriptionm of the form that the lexemes of a token may take ( rule for valid lexemes)

a lexeme is a sequence of characters in the source program that matches the pattern for a token

eg:

if 
else
number
literal 

## lexical errors

some erros cannot be recognized by lexical analyzer.
when no pattern for tokens match, it is error

## error recovery

panic mode: successive characters are ignored until well formed token

delete one char from remaining input
insert missing char into remaining input
replace a char
transpose chars

## input buffering

sometimes analyzer needs to look ahead some symbols
return maximum matching token

## specification of tokens

regex is used to formalize the specification

eg:
letter(letter|digit)* -> must start with a letter and have any number of following letters/digits

regex is a pattern specifying the form of strings


