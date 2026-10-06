#include <stdio.h>
#include <string.h>

char stack[50];
char input[50];
int top = -1;
int ip = 0;

void push(char ch)
{
    stack[++top] = ch;
    stack[top + 1] = '\0';
}

int reduce()
{
    /* E -> a */
    if (top >= 0 && stack[top] == 'a')
    {
        stack[top] = 'E';
        return 1;
    }

    /* E -> b */
    if (top >= 0 && stack[top] == 'b')
    {
        stack[top] = 'E';
        return 1;
    }

    /* E -> E+E */
    if (top >= 2 &&
        stack[top - 2] == 'E' &&
        stack[top - 1] == '+' &&
        stack[top] == 'E')
    {
        top = top - 2;
        stack[top] = 'E';
        stack[top + 1] = '\0';
        return 1;
    }

    /* E -> E*E */
    if (top >= 2 &&
        stack[top - 2] == 'E' &&
        stack[top - 1] == '*' &&
        stack[top] == 'E')
    {
        top = top - 2;
        stack[top] = 'E';
        stack[top + 1] = '\0';
        return 1;
    }

    /* E -> E/E */
    if (top >= 2 &&
        stack[top - 2] == 'E' &&
        stack[top - 1] == '/' &&
        stack[top] == 'E')
    {
        top = top - 2;
        stack[top] = 'E';
        stack[top + 1] = '\0';
        return 1;
    }

    return 0;
}

int main()
{
    int len;

    printf("\n\t\tSHIFT REDUCE PARSER\n");

    printf("\nGRAMMAR");
    printf("\nE -> E+E");
    printf("\nE -> E/E");
    printf("\nE -> E*E");
    printf("\nE -> a/b");

    printf("\n\nEnter the input symbol: ");
    scanf("%s", input);

    len = strlen(input);

    printf("\n\nStack\t\tInput\t\tAction\n");
    printf("---------------------------------------------");

    while (ip < len)
    {
        /* SHIFT */
        push(input[ip]);

        printf("\n$%s\t\t%s$\t\tShift %c",
               stack, input + ip + 1, input[ip]);

        ip++;

        /* REDUCE */
        while (reduce())
        {
            if (stack[top] == 'E')
            {
                printf("\n$%s\t\t%s$\t\tReduce",
                       stack, input + ip);
            }
        }
    }

    /* Final check */
    if (top == 0 && stack[0] == 'E')
    {
        printf("\n$%s\t\t$\t\tACCEPT\n", stack);
    }
    else
    {
        printf("\n$%s\t\t$\t\tREJECT\n", stack);
    }

    return 0;
}
<img width="591" height="667" alt="Screenshot 2026-10-06 104252" src="https://github.com/user-attachments/assets/7e567c16-9775-4872-971e-b27608a40b67" />
