#include <stdio.h>
#include <stdlib.h>
#include <string.h>

char *input;
int i = 0;

char lasthandle[10];
char stack[50];

char handles[][5] = {
    ")E(",
    "E*E",
    "E+E",
    "i",
    "E^E"
};

int top = 0;
int l;

/* Operator precedence table */
char prec[9][9] = {
    /* +   -   *   /   ^   i   (   )   $ */

    /* + */ {'>', '>', '<', '<', '<', '<', '<', '>', '>'},
    /* - */ {'>', '>', '<', '<', '<', '<', '<', '>', '>'},
    /* * */ {'>', '>', '>', '>', '<', '<', '<', '>', '>'},
    /* / */ {'>', '>', '>', '>', '<', '<', '<', '>', '>'},
    /* ^ */ {'>', '>', '>', '>', '<', '<', '<', '>', '>'},
    /* i */ {'>', '>', '>', '>', '>', 'e', 'e', '>', '>'},
    /* ( */ {'<', '<', '<', '<', '<', '<', '<', '>', 'e'},
    /* ) */ {'>', '>', '>', '>', '>', 'e', 'e', '>', '>'},
    /* $ */ {'<', '<', '<', '<', '<', '<', '<', '<', '>'}
};

int getindex(char c)
{
    switch (c)
    {
        case '+': return 0;
        case '-': return 1;
        case '*': return 2;
        case '/': return 3;
        case '^': return 4;
        case 'i': return 5;
        case '(': return 6;
        case ')': return 7;
        case '$': return 8;
    }

    return -1;
}

void shift()
{
    stack[++top] = input[i++];
    stack[top + 1] = '\0';
}

int reduce()
{
    int h, len, found, t;

    for (h = 0; h < 5; h++)
    {
        len = strlen(handles[h]);

        if (top + 1 >= len)
        {
            found = 1;

            for (t = 0; t < len; t++)
            {
                if (stack[top - t] != handles[h][t])
                {
                    found = 0;
                    break;
                }
            }

            if (found)
            {
                stack[top - len + 1] = 'E';
                top = top - len + 1;

                stack[top + 1] = '\0';

                strcpy(lasthandle, handles[h]);

                return 1;
            }
        }
    }

    return 0;
}

void dispstack()
{
    int j;

    for (j = 0; j <= top; j++)
        printf("%c", stack[j]);
}

void dispinput()
{
    int j;

    for (j = i; j < l; j++)
        printf("%c", input[j]);
}

int main()
{
    input = (char *)malloc(50 * sizeof(char));

    if (input == NULL)
    {
        printf("Memory allocation failed");
        return 1;
    }

    printf("\nEnter the string\n");
    scanf("%49s", input);

    strcat(input, "$");
    l = strlen(input);

    strcpy(stack, "$");

    printf("\nSTACK\tINPUT\tACTION");

    while (i < l - 1)
    {
        shift();

        printf("\n");
        dispstack();
        printf("\t");
        dispinput();
        printf("\tShift");

        if (prec[getindex(stack[top])][getindex(input[i])] == '>')
        {
            while (reduce())
            {
                printf("\n");
                dispstack();
                printf("\t");
                dispinput();
                printf("\tReduced: E->%s", lasthandle);
            }
        }
    }

    /* Final reductions */
    while (top > 1 && reduce())
    {
        printf("\n");
        dispstack();
        printf("\t");
        dispinput();
        printf("\tReduced: E->%s", lasthandle);
    }

    /* Accept */
    if (strcmp(stack, "$E") == 0 && input[i] == '$')
    {
        printf("\nAccepted;\n");
    }
    else
    {
        printf("\nNot Accepted;\n");
    }

    free(input);

    return 0;
}
<img width="415" height="647" alt="Screenshot 2026-10-06 104840" src="https://github.com/user-attachments/assets/721465b1-abb7-493d-9ec5-84263b7b6da8" />
