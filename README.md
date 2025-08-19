%{
#include <stdio.h>
#include <stdlib.h>
%}

digit   [0-9]
letter  [A-Za-z_]
id      {letter}({letter}|{digit})*
number  {digit}+

%%
[ \t\n]+                ;
"//".*                  ;
"/*"([^*]|\*+[^*/])*\*+"/"    ;

"int"                   { printf("KEYWORD: %s\n", yytext); }
"float"                 { printf("KEYWORD: %s\n", yytext); }
"char"                  { printf("KEYWORD: %s\n", yytext); }
"return"                { printf("KEYWORD: %s\n", yytext); }
"if"                    { printf("KEYWORD: %s\n", yytext); }
"else"                  { printf("KEYWORD: %s\n", yytext); }
"while"                 { printf("KEYWORD: %s\n", yytext); }

{id}                    { printf("IDENTIFIER: %s\n", yytext); }
{number}                { printf("NUMBER: %s\n", yytext); }

"+"|"-"|"*"|"/"         { printf("OPERATOR: %s\n", yytext); }
"="                     { printf("ASSIGN: %s\n", yytext); }
"=="|"!="|"<"|"<="|">"|">=" { printf("RELATIONAL OP: %s\n", yytext); }

";"                     { printf("SEMICOLON\n"); }
","                     { printf("COMMA\n"); }
"("                     { printf("LPAREN\n"); }
")"                     { printf("RPAREN\n"); }
"{"                     { printf("LBRACE\n"); }
"}"                     { printf("RBRACE\n"); }

.                       { printf("UNKNOWN: %s\n", yytext); }
%%

int main(int argc, char *argv[]) {
    if (argc > 1) {
        FILE *file = fopen(argv[1], "r");
        if (!file) {
            perror("Error opening file");
            return 1;
        }
        yyin = file;
    }
    yylex();
    return 0;
}

int yywrap() {
    return 1;
}
this is lexer.l

flex lexer.l
gcc lex.yy.c -o lexer
./lexer test.c


int main() {
    int a = 5;
    float b = 3.14;
    char c = 'x';

    if (a > b) {
        a = a + 1;
    } else {
        a = a - 1;
    }

    return 0;
}
