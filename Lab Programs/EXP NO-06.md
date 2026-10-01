#include <stdio.h>
#include <ctype.h>
#include <string.h>

int main()
{
    char a[50];
    int flag = 1;
    int i;

    printf("Enter an identifier: ");
    fgets(a, sizeof(a), stdin);

    /* Remove newline */
    a[strcspn(a, "\n")] = '\0';

    /* First character must be a letter */
    if (!isalpha(a[0]))
    {
        flag = 0;
    }
    else
    {
        /* Remaining characters can be letters or digits */
        for (i = 1; a[i] != '\0'; i++)
        {
            if (!isalnum(a[i]))
            {
                flag = 0;
                break;
            }
        }
    }

    if (flag == 1)
        printf("Valid identifier\n");
    else
        printf("Not a valid identifier\n");

    return 0;
}<img width="342" height="163" alt="Screenshot 2026-10-01 140424" src="https://github.com/user-attachments/assets/c325f662-74c3-4970-8123-39f233abac40" />
