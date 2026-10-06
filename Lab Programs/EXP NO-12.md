#include <stdio.h>
#include <string.h>

char input[100];
int i = 0;

int E();
int EP();
int T();
int TP();
int F();

int main()
{
    printf("\nRecursive descent parsing for the following grammar\n");

    printf("\nE  -> TE'");
    printf("\nE' -> +TE' / @");
    printf("\nT  -> FT'");
    printf("\nT' -> *FT' / @");
    printf("\nF  -> (E) / ID\n");

    printf("\nEnter the string to be checked: ");
    scanf("%s", input);

    i = 0;

    if (E())
    {
        if (input[i] == '\0')
            printf("\nString is accepted\n");
        else
            printf("\nString is not accepted\n");
    }
    else
    {
        printf("\nString is not accepted\n");
    }

    return 0;
}

/* E -> TE' */
int E()
{
    if (T())
    {
        if (EP())
            return 1;
    }

    return 0;
}

/* E' -> +TE' / @ */
int EP()
{
    if (input[i] == '+')
    {
        i++;

        if (T())
        {
            return EP();
        }

        return 0;
    }

    return 1;
}

/* T -> FT' */
int T()
{
    if (F())
    {
        if (TP())
            return 1;
    }

    return 0;
}

/* T' -> *FT' / @ */
int TP()
{
    if (input[i] == '*')
    {
        i++;

        if (F())
        {
            return TP();
        }

        return 0;
    }

    return 1;
}

/* F -> (E) / ID */
int F()
{
    /* F -> (E) */
    if (input[i] == '(')
    {
        i++;

        if (E())
        {
            if (input[i] == ')')
            {
                i++;
                return 1;
            }
        }

        return 0;
    }

    /* F -> ID */
    if ((input[i] >= 'a' && input[i] <= 'z') ||
        (input[i] >= 'A' && input[i] <= 'Z'))
    {
        i++;
        return 1;
    }

    return 0;
}
<img width="617" height="440" alt="Screenshot 2026-10-06 103247" src="https://github.com/user-attachments/assets/2970b798-3c0e-40c2-85d0-ed3a7cbdba54" />
