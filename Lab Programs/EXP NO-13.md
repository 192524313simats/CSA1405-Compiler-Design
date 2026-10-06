#include <stdio.h>
#include <string.h>

int main()
{
    char string[50];
    int flag = 0;
    int count;
    int length;

    printf("The grammar is: S->aS, S->Sb, S->ab\n");

    printf("Enter the string to be checked:\n");
    scanf("%s", string);

    length = strlen(string);

    /* String must start with a and end with b */
    if (string[0] != 'a')
    {
        printf("String not accepted");
        return 0;
    }

    for (count = 0; count < length; count++)
    {
        if (string[count] == 'b')
        {
            flag = 1;
        }
        else if (string[count] == 'a')
        {
            if (flag == 1)
            {
                printf("The string does not belong to the specified grammar");
                return 0;
            }
        }
        else
        {
            printf("String not accepted");
            return 0;
        }
    }

    if (flag == 1)
        printf("String accepted");
    else
        printf("String not accepted");

    return 0;
}<img width="448" height="207" alt="Screenshot 2026-10-06 103634" src="https://github.com/user-attachments/assets/db5d9830-0b02-4d03-a6d4-1b6785c7949b" />
