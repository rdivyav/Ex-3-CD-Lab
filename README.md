# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date: 20-09- 2025
# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
flex.l
```
%{
#include "y.tab.h"
%}

digit   [0-9]
%%
[ \t\n]+        ; // Ignore whitespace
{digit}+        { yylval = atoi(yytext); return NUMBER; }
[\+\-\*/]       { return *yytext; }
\(              { return '('; }
\)              { return ')'; }
.               { return 0; }
%%
int yywrap() { return 1; }
```
bison.y
```
%{
#include <stdio.h>
#include <stdlib.h>
void yyerror(const char *s);
int yylex(void);
%}

%token NUMBER

%%
expr:   expr '+' term
        | expr '-' term
        | term
        ;

term:   term '*' factor
        | term '/' factor
        | factor
        ;

factor: '(' expr ')'
        | NUMBER
        ;

%%

```
# OUTPUT
<img width="1475" height="639" alt="Screenshot 2025-09-20 151731" src="https://github.com/user-attachments/assets/5fea8a03-2eb3-4c0f-8998-ddf3202f641c" />

# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
