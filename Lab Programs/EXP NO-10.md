#include <stdio.h>
#include <string.h>

int main()
{
    char gram[50];
    char part1[30], part2[30];
    char modifiedGram[30], newGram[50];

    int i, j, k, pos;

    printf("Enter Production : S->");
    scanf("%s", gram);

    /* Extract first part */
    i = 0;
    j = 0;

    while (gram[i] != '|')
    {
        part1[j++] = gram[i++];
    }
    part1[j] = '\0';

    /* Extract second part */
    i++;
    j = 0;

    while (gram[i] != '\0')
    {
        part2[j++] = gram[i++];
    }
    part2[j] = '\0';

    /* Find common prefix */
    i = 0;
    k = 0;

    while (part1[i] != '\0' &&
           part2[i] != '\0' &&
           part1[i] == part2[i])
    {
        modifiedGram[k++] = part1[i];
        i++;
    }

    pos = i;

    /* Add new non-terminal X */
    modifiedGram[k++] = 'X';
    modifiedGram[k] = '\0';

    /* Create new production */
    j = 0;

    for (i = pos; part1[i] != '\0'; i++)
    {
        newGram[j++] = part1[i];
    }

    newGram[j++] = '|';

    for (i = pos; part2[i] != '\0'; i++)
    {
        newGram[j++] = part2[i];
    }

    newGram[j] = '\0';

    /* Display result */
    printf("\nS->%s", modifiedGram);
    printf("\nX->%s\n", newGram);

    return 0;
}
<img width="372" height="203" alt="Screenshot 2026-10-06 100731" src="https://github.com/user-attachments/assets/24692e2d-56c5-4844-a849-bc05266558c1" />
