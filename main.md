lab_7_Kohovich-MS
=================
#include <stdio.h>
/*Имеется список учета нуждающихся в улучшении жилищных условий. 
Каждая запись этого списка содержит фамилию, имя, отчество и дату постановки на учет.
 Список упорядочен по дате постановки на учет. Известно число квартир, выделяемых по данному 
списку в течение года. Рассчитать, какое количество лет в среднем необходимо ожидать получения квартиры, 
и вывести на экран весь список с указанием ожидаемого года получения квартиры.*/
struct fio
{
    char surname[15];
    char name[15];
    char patronymic[15];
};

struct nuzhd
{
    struct fio inf;
    int yearpost;
    int zhdyears;
    int yearpol;
};

struct nuzhd spisok[20];
int kol;

int main(int argc, char* argv[])
{
    printf("Лабораторная работа №7\nВыполнил студент гр.107512 Кохович М.С.\n");
    int a;
    int zagod;
    int yearnow;
    printf("Введите колличество квартир сдаваемых за год: ");
    scanf("%d",&zagod);
    int i,j;
    kol = 0;
    char ent;
    while(a)
    {
        int sredn = 0;
        yearnow = 2013;
        printf("Введите 1, если хотите добавить запись в список, введите 2 для получения\nинформации по кравтирам, введите 0 для выхода из программы:");
        scanf("%d",&a);
        scanf("%c",&ent);
        switch(a)
        {
        case 0:
        {
            return 0;
            break;
        }
        case 1:
        {
            inp(kol);
            scanf("%c",&ent);
            break;
        }
        case 2:
        {
            sort();
            i = 0;
            int g = 0;
            while (i < kol)
            {
                for(j = 0; j < zagod && i < kol; j++,i++)
                {
                    spisok[i].yearpol = yearnow + g;
                    spisok[i].zhdyears = spisok[i].yearpol - spisok[i].yearpost;
                    sredn += spisok[i].zhdyears;
                }
                g++;
            }
            sredn = sredn / kol;
            for (i = 0; i < kol; i++)
            {
                outp(i);
            }
            printf("-----------------------------------\n");
            printf("Среднее время ожидания квартиры: %d лет(года).\n",sredn);
            break;
        }
        }
    }

    return 0;
}

int inp(int index)
{
    printf("Введите фамилию: ");
    gets(spisok[index].inf.surname);
    printf("Введите имя: ");
    gets(spisok[index].inf.name);
    printf("Введите отчество: ");
    gets(spisok[index].inf.patronymic);
    printf("Введите год постановки на учет: ");
    scanf("%d",&spisok[index].yearpost);
    kol++;
    return 0;
}

int outp(int index)
{
    printf("------------------------\n");
    printf("Фамилия: %s\n",spisok[index].inf.surname);
    printf("Имя: %s\n", spisok[index].inf.name);
    printf("Отчество: %s\n",spisok[index].inf.patronymic);
    printf("Поставлен на учет: %d г.\n", spisok[index].yearpost);
    printf("Получит квартиру: %d\n", spisok[index].yearpol);
    return 0;
}

int sort(void)
{
    int i;
    int exchange;
    int a,b;
    struct nuzhd buff;
    for (i = 0; i < kol - 1; i++)
    {
        exchange = 0;
        a = i;
        for(b = a+1; b < kol; b++)
        {
            if(spisok[b].yearpost < spisok[a].yearpost)
            {
                buff = spisok[b];
                a = b;
                exchange++;
            }
        }
        if (exchange)
        {
            spisok[a] = spisok[i];
            spisok[i] = buff;
        }
    }
    return 0;
}




