#include <stdio.h>
#include <string.h>

#define SIZE 10

int main()
{
    char non_terminal;
    char beta, alpha;
    int num;
    char production[10][SIZE];
    int index;

    printf("Enter Number of Production : ");
    scanf("%d", &num);

    printf("Enter the grammar as E->E-A|B :\n");

    for (int i = 0; i < num; i++)
    {
        scanf("%s", production[i]);
    }

    for (int i = 0; i < num; i++)
    {
        printf("\nGRAMMAR : : : %s", production[i]);

        non_terminal = production[i][0];
        index = 3;   /* Starting position after -> */

        /* Check for left recursion */
        if (non_terminal == production[i][index])
        {
            alpha = production[i][index + 1];

            printf(" is left recursive.\n");

            /* Find | */
            while (production[i][index] != '\0' &&
                   production[i][index] != '|')
            {
                index++;
            }

            if (production[i][index] != '\0')
            {
                beta = production[i][index + 1];

                printf("Grammar without left recursion:\n");

                printf("%c->%c%c'\n",
                       non_terminal, beta, non_terminal);

                printf("%c'->%c%c'|E\n",
                       non_terminal, alpha, non_terminal);
            }
            else
            {
                printf(" can't be reduced\n");
            }
        }
        else
        {
            printf(" is not left recursive.\n");
        }
    }

    return 0;
}
<img width="546" height="328" alt="Screenshot 2026-10-06 100349" src="https://github.com/user-attachments/assets/ee2a1f75-246d-482f-90cd-56b79ba36d48" />
