# Practical-task-8
#include <stdio.h>
#include <string.h>

// Функція для обчислення факторіалу числа
int factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;
    } else {
        return n * factorial(n - 1);
    }
}

// Функція для обчислення кількості анаграм
int calculateAnagramCount(char word[]) {
    int length = strlen(word);

    // Обчислюємо кількість анаграм за формулою: факторіал(length) / (кількість_повторень_букв_1! * кількість_повторень_букв_2! * ...)
    int count = factorial(length);
    int letterCount[26] = {0}; // Масив для підрахунку кількості повторень кожної букви

    // Підраховуємо кількість повторень кожної букви у слові
    for (int i = 0; i < length; i++) {
        char c = toupper(word[i]); // Перетворюємо букву у верхній регістр
        if (c >= 'A' && c <= 'Z') { // Перевіряємо, чи символ є літерою
            int index = c - 'A'; // Перетворюємо букву у відповідний індекс (від 0 до 25)
            letterCount[index]++;
        }
    }

    // Обчислюємо ділення факторіал(length) на добуток факторіалів кількостей повторень кожної букви
    for (int i = 0; i < 26; i++) {
        if (letterCount[i] > 1) {
            count /= factorial(letterCount[i]);
        }
    }

    return count;
}

int main() {
    char word[15];

    printf("Введіть слово: ");
    scanf("%s", word);

    int anagramCount = calculateAnagramCount(word);

    printf("Кількість анаграм: %d\n", anagramCount);

    return 0;
}
