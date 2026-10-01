#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

int isKeyword(char buffer[])
{
    char keywords[32][10] = {
        "main", "auto", "break", "case", "char", "const",
        "continue", "default", "do", "double", "else", "enum",
        "extern", "float", "for", "goto", "if", "int", "long",
        "register", "return", "short", "signed", "sizeof",
        "static", "struct", "switch", "typedef", "unsigned",
        "void", "printf", "while"
    };

    int i;

    for (i = 0; i < 32; i++)
    {
        if (strcmp(keywords[i], buffer) == 0)
        {
            return 1;
        }
    }

    return 0;
}

int main()
{
    char input[] =
        "main ( ) {\n"
        "int a, b, c;\n"
        "c = b + c;\n"
        "printf ( \"%d\", c );\n"
        "}";

    char ch, next;
    char buffer[100];
    char operators[] = "+-*/%=";
    int i, j = 0;
    int length = strlen(input);

    for (i = 0; i < length; i++)
    {
        ch = input[i];

        /* Ignore single-line comments */
        if (ch == '/' && i + 1 < length && input[i + 1] == '/')
        {
            i += 2;

            while (i < length && input[i] != '\n')
            {
                i++;
            }

            continue;
        }

        /* Ignore multi-line comments */
        if (ch == '/' && i + 1 < length && input[i + 1] == '*')
        {
            i += 2;

            while (i + 1 < length &&
                   !(input[i] == '*' && input[i + 1] == '/'))
            {
                i++;
            }

            i++;
            continue;
        }

        /* Identify operators */
        for (int k = 0; k < 6; k++)
        {
            if (ch == operators[k])
            {
                printf("%c is operator\n", ch);
                break;
            }
        }

        /* Identify words */
        if (isalnum((unsigned char)ch) || ch == '_')
        {
            buffer[j++] = ch;
        }
        else if (isspace((unsigned char)ch) && j != 0)
        {
            buffer[j] = '\0';
            j = 0;

            if (isKeyword(buffer))
            {
                printf("%s is keyword\n", buffer);
            }
            else
            {
                printf("%s is identifier\n", buffer);
            }
        }
    }

    /* Process the last token */
    if (j != 0)
    {
        buffer[j] = '\0';

        if (isKeyword(buffer))
        {
            printf("%s is keyword\n", buffer);
        }
        else
        {
            printf("%s is identifier\n", buffer);
        }
    }

    return 0;
}
<img width="257" height="487" alt="Screenshot 2026-10-01 135225" src="https://github.com/user-attachments/assets/6b3460e8-c046-44d9-b192-9fe0938383a9" />



<img width="257" height="487" alt="Screenshot 2026-10-01 135225" src="https://github.com/user-attachments/assets/945722ba-e86f-47c5-a0c3-fa3e937788c3" />
