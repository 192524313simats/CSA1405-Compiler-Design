#include <stdio.h>
#include <ctype.h>
#include <string.h>

int limit, x = 0;
char production[10][10], array[10];

void find_first(char ch);
void find_follow(char ch);
void Array_Manipulation(char ch);

int main()
{
    int count;
    char option, ch;

    printf("\nEnter Total Number of Productions:\t");
    scanf("%d", &limit);

    for (count = 0; count < limit; count++)
    {
        printf("\nValue of Production Number [%d]:\t", count + 1);
        scanf("%s", production[count]);
    }

    do
    {
        x = 0;

        printf("\nEnter production Value to Find Follow:\t");
        scanf(" %c", &ch);

        find_follow(ch);

        printf("\nFollow Value of %c:\t{ ", ch);

        for (count = 0; count < x; count++)
        {
            printf("%c ", array[count]);
        }

        printf("}\n");

        printf("To Continue, Press Y:\t");
        scanf(" %c", &option);

    } while (option == 'y' || option == 'Y');

    return 0;
}

void find_follow(char ch)
{
    int i, j, length;

    /* Start symbol gets $ */
    if (production[0][0] == ch)
    {
        Array_Manipulation('$');
    }

    for (i = 0; i < limit; i++)
    {
        length = strlen(production[i]);

        for (j = 2; j < length; j++)
        {
            if (production[i][j] == ch)
            {
                /* If a symbol exists after ch */
                if (production[i][j + 1] != '\0')
                {
                    find_first(production[i][j + 1]);
                }

                /* If ch is at the end */
                if (production[i][j + 1] == '\0' &&
                    ch != production[i][0])
                {
                    find_follow(production[i][0]);
                }
            }
        }
    }
}

void find_first(char ch)
{
    int i;

    /* If terminal */
    if (!isupper(ch))
    {
        if (ch != '$')
        {
            Array_Manipulation(ch);
        }
        return;
    }

    /* If non-terminal */
    for (i = 0; i < limit; i++)
    {
        if (production[i][0] == ch)
        {
            /* If epsilon production */
            if (production[i][2] == '$')
            {
                find_follow(production[i][0]);
            }
            /* If terminal */
            else if (!isupper(production[i][2]))
            {
                Array_Manipulation(production[i][2]);
            }
            /* If non-terminal */
            else
            {
                find_first(production[i][2]);
            }
        }
    }
}

void Array_Manipulation(char ch)
{
    int count;

    for (count = 0; count < x; count++)
    {
        if (array[count] == ch)
        {
            return;
        }
    }
    <img width="555" height="500" alt="Screenshot 2026-10-06 095921" src="https://github.com/user-attachments/assets/400fb8b3-4bab-4dfb-9b80-ce90c8058daa" />


    array[x++] = ch;
}
