# Домашнее задание к работе 19
## Условие задачи
Вариант 4. Запись «Киносеанс»:
Название фильма
Дата и время сеанса
Продолжительность сеанса
Жанр
Бюджет


## 1. Алгоритм и блок-схема
## Алгоритм
```
1. Начало программы
2. Создаем структуру kinoseans с полями: название фильма, жанр, дата, время, бюджет
3. Вводим количество сеансов
4. Выделяем динамическую память под массив структур
5. Заполняем массив данными о киносеансах с клавиатуры
6. Вызываем функцию writefile() для записи в файл "seans.txt"
7. Функция writefile() открывает файл и записывает данные в форматированном виде
8. Освобождаем память и выводим сообщение об успешной записи
9. Конец программы

```
   
### Блок-схема

<img width="330" height="1214" alt="image" src="https://github.com/user-attachments/assets/015179cb-0ae1-45f1-aa71-ee38fd0bc696" />


## 2. Реализация программы

```
#define _CRT_SECURE_NO_WARNINGS
#include <stdio.h>
#include <locale.h>
#include <stdlib.h>

typedef struct {
    char filmname[20];
    char genre[20];
    int day;
    int month;
    int year;
    int hour;
    int minute;
    int budg;
} kinoseans;

int writefile(char* fname, kinoseans* kino, int size) {
    FILE* out;
    if ((out = fopen(fname, "wt")) == NULL) {
        printf("Ошибка открытия файла для записи\n");
        return 0;
    }

    for (int i = 0; i < size; i++) {
        fprintf(out, "Имя:%20s ; Жанр:%20s ; Дата: %2d.%2d.%4d; Время:%2d:%2d; Бюджет:%d\n",
            kino[i].filmname, kino[i].genre, kino[i].day, kino[i].month,
            kino[i].year, kino[i].hour, kino[i].minute, kino[i].budg);
    }

    fclose(out);
    return 1;
}

int main() {
    setlocale(LC_ALL, "RUS");

    int n;
    printf("Введите количество сеансов: ");
    scanf("%d", &n);

    kinoseans* seansy = (kinoseans*)malloc(n * sizeof(kinoseans));

    for (int i = 0; i < n; i++) {
        printf("\nСеанс №%d\n", i + 1);
        printf("Название фильма (без пробелов): ");
        scanf("%s", seansy[i].filmname);
        printf("Жанр (без пробелов): ");
        scanf("%s", seansy[i].genre);
        printf("Дата (день месяц год через пробел): ");
        scanf("%d %d %d", &seansy[i].day, &seansy[i].month, &seansy[i].year);
        printf("Время (часы минуты через пробел): ");
        scanf("%d %d", &seansy[i].hour, &seansy[i].minute);
        printf("Бюджет: ");
        scanf("%d", &seansy[i].budg);
    }

    if (writefile("seans.txt", seansy, n)) {
        printf("\nДанные успешно записаны в файл seans.txt\n");
    }

    free(seansy);
    system("pause");
    return 0;
}
```


## 3. Результаты работы программы

```
Введите количество сеансов: 2

Сеанс №1
Название фильма (без пробелов): Бурундуки
Жанр (без пробелов): Ужасы
Дата (день месяц год через пробел): 29 08 2007
Время (часы минуты через пробел): 1 36
Бюджет: 300000

Сеанс №2
Название фильма (без пробелов): Коты
Жанр (без пробелов): Комедия
Дата (день месяц год через пробел): 8 29 2006
Время (часы минуты через пробел): 3 16
Бюджет: 500000

Данные успешно записаны в файл seans.txt
Для продолжения нажмите любую клавишу . . .
```

<img width="685" height="543" alt="image" src="https://github.com/user-attachments/assets/96b85386-75fa-4668-bd19-f2cc0119b060" />

