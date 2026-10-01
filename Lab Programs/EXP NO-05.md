#include <stdio.h>
#include <ctype.h>

int main()
{
    char str[500];
    int words = 0;
    int lines = 0;
    int characters = 0;
    int inWord = 0;
    int i;

    printf("Enter text (enter ~ to end):\n");

    i = 0;

    while (1)
    {
        char ch = getchar();

        if (ch == '~')
            break;

        str[i] = ch;
        i++;
    }

    str[i] = '\0';

    for (i = 0; str[i] != '\0'; i++)
    {
        if (str[i] == '\n')
        {
            lines++;
        }

        if (isspace(str[i]))
        {
            inWord = 0;
        }
        else
        {
            characters++;

            if (inWord == 0)
            {
                words++;
                inWord = 1;
            }
        }
    }

    if (characters > 0 && lines == 0)
    {
        lines = 1;
    }
    else if (characters > 0 && str[i - 1] != '\n')
    {
        lines++;
    }

    printf("\nTotal number of words: %d", words);
    printf("\nTotal number of lines: %d", lines);
    printf("\nTotal number of characters: %d", characters);

    return 0;
}<img width="442" height="438" alt="Screenshot 2026-10-01 140100" src="https://github.com/user-attachments/assets/d16c12a0-abeb-4536-b264-735b86b364bc" />
