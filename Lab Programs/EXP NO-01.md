#include <stdio.h>
#include <ctype.h>
#include <string.h>

int main()
{
    int i, ic = 0, cc = 0, oc = 0;
    int m;
    char b[100];
    char operators[30];
    char identifiers[30];
    int constants[30];

    printf("Enter the string: ");
    scanf("%[^\n]", b);

    for (i = 0; i < strlen(b); i++)
    {
        if (isspace(b[i]))
        {
            continue;
        }

        else if (isalpha(b[i]))
        {
            identifiers[ic] = b[i];
            ic++;
        }

        else if (isdigit(b[i]))
        {
            m = 0;

            while (isdigit(b[i]))
            {
                m = m * 10 + (b[i] - '0');
                i++;
            }

            i--;
            constants[cc] = m;
            cc++;
        }

        else
        {
            if (b[i] == '*' || b[i] == '-' ||
                b[i] == '+' || b[i] == '=')
            {
                operators[oc] = b[i];
                oc++;
            }
        }
    }

    printf("\nIdentifiers : ");
    for (i = 0; i < ic; i++)
    {
        printf("%c ", identifiers[i]);
    }

    printf("\nConstants : ");
    for (i = 0; i < cc; i++)
    {
        printf("%d ", constants[i]);
    }

    printf("\nOperators : ");
    for (i = 0; i < oc; i++)
    {
        printf("%c ", operators[i]);
    }

    return 0;
}
<img width="442" height="247" alt="Screenshot 2026-10-01 133640" src="https://github.com/user-attachments/assets/9edd74b0-d631-4ca3-ab60-f03d4c8d7fac" />


OUTPUT:

