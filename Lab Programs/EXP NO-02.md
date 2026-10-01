#include <stdio.h>
#include <string.h>

int main()
{
    char com[100];
    int i, a = 0;

    printf("Enter comment: ");
    fgets(com, sizeof(com), stdin);

    if (com[0] == '/' && com[1] == '/')
    {
        printf("It is a comment");
    }
    else if (com[0] == '/' && com[1] == '*')
    {
        for (i = 2; i < strlen(com) - 1; i++)
        {
            if (com[i] == '*' && com[i + 1] == '/')
            {
                a = 1;
                break;
            }
        }

        if (a == 1)
            printf("It is a comment");
        else
            printf("It is not a comment");
    }
    else
    {
        printf("It is not a comment");
    }

    return 0;
}
<img width="312" height="166" alt="Screenshot 2026-10-01 134549" src="https://github.com/user-attachments/assets/0d8df15d-4bb4-4fca-a8bc-51ba7e4120c3" />
<img width="306" height="152" alt="Screenshot 2026-10-01 134717" src="https://github.com/user-attachments/assets/57e61917-1944-4b9b-af36-7cc8740b0ffd" />


<img width="312" height="166" alt="Screenshot 2026-10-01 134549" src="https://github.com/user-attachments/assets/e4ec125c-7731-4268-a804-a2cfd488e7a9" />
