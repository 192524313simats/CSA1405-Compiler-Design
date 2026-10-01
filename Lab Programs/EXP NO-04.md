#include <stdio.h>
#include <string.h>

int main()
{
    char s[5];

    printf("Enter any operator: ");
    scanf("%4s", s);

    switch (s[0])
    {
        case '>':
            if (s[1] == '=')
                printf("Greater than or equal");
            else
                printf("Greater than");
            break;

        case '<':
            if (s[1] == '=')
                printf("Less than or equal");
            else
                printf("Less than");
            break;

        case '=':
            if (s[1] == '=')
                printf("Equal to");
            else
                printf("Assignment");
            break;

        case '!':
            if (s[1] == '=')
                printf("Not Equal");
            else
                printf("Bit Not");
            break;

        case '&':
            if (s[1] == '&')
                printf("Logical AND");
            else
                printf("Bitwise AND");
            break;

        case '|':
            if (s[1] == '|')
                printf("Logical OR");
            else
                printf("Bitwise OR");
            break;

        case '+':
            printf("Addition");
            break;

        case '-':
            printf("Subtraction");
            break;

        case '*':
            printf("Multiplication");
            break;

        case '/':
            printf("Division");
            break;

        case '%':
            printf("Modulus");
            break;

        default:
            printf("Not an operator");
    }

    return 0;
}

<img width="282" height="160" alt="Screenshot 2026-10-01 135821" src="https://github.com/user-attachments/assets/93eaf350-2ab5-4fb2-bbe8-15cfc5570234" />


