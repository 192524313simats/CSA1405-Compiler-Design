#include <stdio.h>
#include <stdlib.h>
#include <string.h>

int cnt = 0;

struct symtab
{
    char label[20];
    int addr;
} sy[50];

void insert();
int search(char *);
void display();
void modify();

int main()
{
    int ch, val;
    char lab[20];

    do
    {
        printf("\n1.insert");
        printf("\n2.display");
        printf("\n3.search");
        printf("\n4.modify");
        printf("\n5.exit");
        printf("\n");

        scanf("%d", &ch);

        switch(ch)
        {
            case 1:
                insert();
                break;

            case 2:
                display();
                break;

            case 3:
                printf("enter the label: ");
                scanf("%s", lab);

                val = search(lab);

                if(val == 1)
                    printf("label is found\n");
                else
                    printf("label is not found\n");

                break;

            case 4:
                modify();
                break;

            case 5:
                exit(0);

            default:
                printf("Invalid choice\n");
        }

    } while(ch < 5);

    return 0;
}

void insert()
{
    int val;
    char lab[20];

    printf("enter the label: ");
    scanf("%s", lab);

    val = search(lab);

    if(val == 1)
    {
        printf("duplicate symbol\n");
    }
    else
    {
        strcpy(sy[cnt].label, lab);

        printf("enter the address: ");
        scanf("%d", &sy[cnt].addr);

        cnt++;
    }
}

int search(char *s)
{
    int flag = 0;
    int i;

    for(i = 0; i < cnt; i++)
    {
        if(strcmp(sy[i].label, s) == 0)
        {
            flag = 1;
            break;
        }
    }

    return flag;
}

void modify()
{
    int val, ad, i;
    char lab[20];

    printf("enter the label: ");
    scanf("%s", lab);

    val = search(lab);

    if(val == 0)
    {
        printf("no such symbol\n");
    }
    else
    {
        printf("label is found\n");

        printf("enter the address: ");
        scanf("%d", &ad);

        for(i = 0; i < cnt; i++)
        {
            if(strcmp(sy[i].label, lab) == 0)
            {
                sy[i].addr = ad;
            }
        }
    }
}

void display()
{
    int i;

    for(i = 0; i < cnt; i++)
    {
        printf("%s\t%d\n", sy[i].label, sy[i].addr);
    }
}
<img width="550" height="802" alt="Screenshot 2026-10-06 102723" src="https://github.com/user-attachments/assets/2821ad7c-076d-4aec-a115-15ed0d57b8eb" />
