# C++ builder

1 practice lab

void __fastcall TForm1::Button1Click(TObject *Sender)
{
    double x, y, z, t;
    x = -4.5;            // Заданное значение X
    y = 0.75e-4;         // Заданное значение Y (0.000075)
    z = 0.845e2;         // Заданное значение Z (84.5)
    t = 0.564849;        // Заданное значение T

    Memo1->Lines->Add("x=" + FloatToStr(x)); // Вывод X в окно Memo1
    Memo1->Lines->Add("y=" + FloatToStr(y)); // Вывод Y в окно Memo1
    Memo1->Lines->Add("z=" + FloatToStr(z)); // Вывод Z в окно Memo1
    Memo1->Lines->Add("t=" + FloatToStr(t)); // Вывод T в окно Memo1

    // Вычисляем арифметическое выражение
    double term1 = -sin(x + y) + 2;
    double term2 = pow(x * x + y * y, 1.0 / 3); // Кубический корень
    double term3 = z - t * tan(exp(x * y)) + 3 * x;
    double term4 = y * y + z * z;
    double term5 = 2 * x * y * y + z;
    double u = -(term1 / term2) + 18 + (term3 / term4) + term5;

    // Выводим результат в окно Memo1
    Memo1->Lines->Add("Результат U = " + FloatToStrF(u, ffFixed, 8, 3));
}





17 задание 

#include <vcl.h>
#include <iostream>
#pragma hdrstop
#pragma argsused

#include <tchar.h>
#include <stdio.h>

void calculateEndTime(int startHour, int startMinute, int durationHour, int durationMinute, int &endHour, int &endMinute)
{
    // Сложение минут и часов
    endMinute = startMinute + durationMinute;
    endHour = startHour + durationHour + (endMinute / 60); // Учитываем перенос минут в часы
    endMinute = endMinute % 60;                           // Оставляем только минуты в диапазоне 0-59
    endHour = endHour % 24;                               // Учитываем 24-часовой формат
}

int main()
{
    int startHour, startMinute, durationHour, durationMinute;
    int endHour, endMinute;

    // Ввод данных
    printf("Введите время начала рабочего дня (часы минуты): ");
    scanf("%d %d", &startHour, &startMinute);

    printf("Введите продолжительность рабочего дня (часы минуты): ");
    scanf("%d %d", &durationHour, &durationMinute);

    // Вычисление времени окончания
    calculateEndTime(startHour, startMinute, durationHour, durationMinute, endHour, endMinute);

    // Вывод результата
    printf("Время окончания рабочего дня: %02d:%02d\n", endHour, endMinute);

    return 0;
}

2 practice lab 

17 вариант 

#include <vcl.h>
#pragma hdrstop
#include <tchar.h>
#include <stdio.h>

void determineSeason(int month)
{
    if (month >= 3 && month <= 5) 
    {
        printf("Весна\n");
    }
    else if (month >= 6 && month <= 8) 
    {
        printf("Лето\n");
    }
    else if (month >= 9 && month <= 11) 
    {
        printf("Осень\n");
    }
    else if (month == 12 || month <= 2) 
    {
        printf("Зима\n");
    }
    else
    {
        printf("Неверный номер месяца\n");
    }
}

int main()
{
    int month;
    printf("Введите номер месяца (1-12): ");
    scanf("%d", &month);

    determineSeason(month);

    return 0;
}

3 practice lab 

В задаче 33 мы находим максимальное и минимальное числа, а затем вычисляем разницу.
В задаче 34 мы ищем минимальное число и его индекс, при этом 0 завершает последовательность.
В задаче 35 находим максимальное отрицательное число среди всех введенных чисел.
В задаче 36 проверяем, является ли последовательность чисел возрастающей, то есть каждое следующее число должно быть больше предыдущего.

33 вариант 

#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
//---------------------------------------------------------------------------

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}
//---------------------------------------------------------------------------

void __fastcall TForm1::FormCreate(TObject *Sender)
{
    Memo1->Clear();
    Memo1->Lines->Add("Результаты ст. гр.920201 Петрова И.И.");
}
//---------------------------------------------------------------------------

void __fastcall TForm1::Button1Click(TObject *Sender)
{
    int n = StrToInt(Edit1->Text); // Считываем количество чисел
    double number, max, min;
    max = -DBL_MAX;  // Инициализируем переменную для максимума
    min = DBL_MAX;   // Инициализируем переменную для минимума
    
    for (int i = 0; i < n; i++) {
        number = StrToFloat(Edit2->Text); // Считываем очередное число
        if (number > max) max = number;   // Если число больше максимума, обновляем максимум
        if (number < min) min = number;   // Если число меньше минимума, обновляем минимум
    }

    double difference = max - min;  // Вычисляем разность
    Memo1->Lines->Add("Разность между максимальным и минимальным числом: " + FloatToStr(difference));
}


 34 вариант

 #include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
//---------------------------------------------------------------------------

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}
//---------------------------------------------------------------------------

void __fastcall TForm1::FormCreate(TObject *Sender)
{
    Memo1->Clear();
    Memo1->Lines->Add("Результаты ст. гр.920201 Петрова И.И.");
}
//---------------------------------------------------------------------------

void __fastcall TForm1::Button1Click(TObject *Sender)
{
    double number;
    int index = 1;  // Позиция числа
    int minIndex = 0; // Индекс минимального числа
    double min = DBL_MAX;  // Изначально минимальное число очень большое
    
    while (true) {
        number = StrToFloat(Edit2->Text); // Считываем очередное число
        if (number == 0) break; // Выход, если число 0
        if (number < min) {
            min = number;
            minIndex = index;
        }
        index++;  // Увеличиваем индекс
    }

    Memo1->Lines->Add("Порядковый номер наименьшего числа: " + IntToStr(minIndex));
}

35 вариант

#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
//---------------------------------------------------------------------------

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}
//---------------------------------------------------------------------------

void __fastcall TForm1::FormCreate(TObject *Sender)
{
    Memo1->Clear();
    Memo1->Lines->Add("Результаты ст. гр.920201 Петрова И.И.");
}
//---------------------------------------------------------------------------

void __fastcall TForm1::Button1Click(TObject *Sender)
{
    int n = StrToInt(Edit1->Text);  // Считываем количество чисел
    double number, maxNegative = -DBL_MAX;
    
    for (int i = 0; i < n; i++) {
        number = StrToFloat(Edit2->Text); // Считываем очередное число
        if (number < 0 && number > maxNegative) {  // Если число отрицательное и больше найденного
            maxNegative = number;
        }
    }

    Memo1->Lines->Add("Наибольшее среди отрицательных чисел: " + FloatToStr(maxNegative));
}

36 вариант 

#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
//---------------------------------------------------------------------------

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}
//---------------------------------------------------------------------------

void __fastcall TForm1::FormCreate(TObject *Sender)
{
    Memo1->Clear();
    Memo1->Lines->Add("Результаты ст. гр.920201 Петрова И.И.");
}
//---------------------------------------------------------------------------

void __fastcall TForm1::Button1Click(TObject *Sender)
{
    int n = StrToInt(Edit1->Text); // Считываем количество чисел
    double number, prevNumber;
    bool isIncreasing = true;

    for (int i = 0; i < n; i++) {
        number = StrToFloat(Edit2->Text);  // Считываем очередное число
        if (i > 0 && number <= prevNumber) {
            isIncreasing = false;  // Если текущее число не больше предыдущего
            break;
        }
        prevNumber = number;  // Запоминаем текущее число
    }

    if (isIncreasing) {
        Memo1->Lines->Add("Числа образуют возрастающую последовательность.");
    } else {
        Memo1->Lines->Add("Числа не образуют возрастающую последовательность.");
    }
}

4 practice lab 

2 вариант

Задана матрица размером NxM. Получить массив B, присвоив его k-му
элементу значение 1, если элементы k–й строки матрицы упорядочены по
убыванию, и значение 0 − в противном случае.

#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
//---------------------------------------------------------------------------

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}

// Максимальная размерность матрицы
const int Nmax = 10;
int N = 3; // Количество строк
int M = 3; // Количество столбцов
typedef double mas2[Nmax][Nmax];  // Двумерный массив
typedef int mas1[Nmax];           // Одномерный массив для B

mas2 matrix;  // Матрица
mas1 B;        // Массив B

// Функция для проверки, отсортирована ли строка по убыванию
bool IsDecreasing(const mas2& mat, int row, int M)
{
    for (int i = 1; i < M; i++) {
        if (mat[row][i] > mat[row][i-1]) {
            return false;  // Если элемент больше предыдущего, то не по убыванию
        }
    }
    return true;
}

void __fastcall TForm1::FormCreate(TObject *Sender)
{
    // Инициализация данных
    Edit1->Text = FloatToStr(N);  // Количество строк
    Edit2->Text = FloatToStr(M);  // Количество столбцов
    StringGrid1->ColCount = M + 1;
    StringGrid1->RowCount = N + 1;
    StringGrid2->RowCount = N + 1;

    // Заполнение названия массивов
    StringGrid1->Cells[0][0] = "Матрица";
    StringGrid2->Cells[0][0] = "Массив B";

    for (int i = 1; i <= N; i++) {
        StringGrid1->Cells[0][i] = "i=" + IntToStr(i);
        StringGrid1->Cells[i][0] = "j=" + IntToStr(i);
    }
}

// Обработчик нажатия кнопки "Button1" (заполнение матрицы и расчет массива B)
void __fastcall TForm1::Button1Click(TObject *Sender)
{
    // Ввод матрицы из StringGrid1
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < M; j++) {
            matrix[i][j] = StrToFloat(StringGrid1->Cells[j+1][i+1]);
        }
    }

    // Проверка строк матрицы и заполнение массива B
    for (int i = 0; i < N; i++) {
        B[i] = IsDecreasing(matrix, i, M) ? 1 : 0;  // Если строка отсортирована по убыванию, ставим 1, иначе 0
    }

    // Вывод массива B в StringGrid2
    for (int i = 0; i < N; i++) {
        StringGrid2->Cells[0][i+1] = IntToStr(B[i]);
    }
}

17 вариант 

#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
//---------------------------------------------------------------------------

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}

// Обработчик нажатия кнопки "Button1"
void __fastcall TForm1::Button1Click(TObject *Sender)
{
    String inputText = Edit1->Text;  // Чтение текста из Edit1
    
    // Удаление точки с конца строки
    if (inputText.Length() > 0 && inputText[inputText.Length()] == '.') {
        inputText = inputText.SubString(1, inputText.Length() - 1);
    }

    // Разворот строки
    String reversedText = "";
    for (int i = inputText.Length(); i > 0; i--) {
        reversedText += inputText[i];
    }

    // Вывод в Memo1
    Memo1->Lines->Add(reversedText);
}

5 practice lab 

2 вариант

Дана строка, состоящая из групп нулей и единиц. Найти и вывести на
экран самую короткую группу

#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
#include <string>
#include <vector>
#include <algorithm>
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
//---------------------------------------------------------------------------

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}

// Обработчик нажатия кнопки
void __fastcall TForm1::Button1Click(TObject *Sender)
{
    String input = Edit1->Text;  // Получаем строку из поля ввода
    String currentGroup = "";     // Текущая группа (нулей или единиц)
    String shortestGroup = "";    // Самая короткая группа
    int minLength = input.Length() + 1;  // Длина самой короткой группы (изначально больше максимальной возможной)

    // Проходим по строке
    for (int i = 1; i <= input.Length(); i++)
    {
        // Если символ тот же, что и в предыдущей группе, добавляем его
        if (currentGroup.IsEmpty() || input[i-1] == currentGroup[1])
        {
            currentGroup += input[i-1];
        }
        else
        {
            // Если группа закончилась, проверяем, является ли она самой короткой
            if (currentGroup.Length() < minLength)
            {
                minLength = currentGroup.Length();
                shortestGroup = currentGroup;
            }
            // Начинаем новую группу
            currentGroup = input[i-1];
        }
    }

    // Проверяем последнюю группу
    if (currentGroup.Length() < minLength)
    {
        shortestGroup = currentGroup;
    }

    // Выводим самую короткую группу
    Memo1->Lines->Add("Самая короткая группа: " + shortestGroup);
}

17 вариант 

Дана строка символов, состоящая из произвольного текста, слова
разделены пробелами. Удалить первые k слов из строки, сдвинув на их место
последующие.


#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
#include <vector>
#include <sstream>
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;
//---------------------------------------------------------------------------

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}

// Обработчик нажатия кнопки
void __fastcall TForm1::Button1Click(TObject *Sender)
{
    String input = Edit1->Text;  // Получаем строку из поля ввода
    int k = StrToInt(Edit2->Text); // Получаем значение k из другого поля ввода

    // Преобразуем String в std::string для удобства работы с пробелами
    std::string str = input.c_str();

    // Разделяем строку на слова
    std::stringstream ss(str);
    std::string word;
    std::vector<std::string> words;

    while (ss >> word)  // Читаем по словам
    {
        words.push_back(word);
    }

    // Проверка, чтобы k не превышало количество слов
    if (k >= words.size()) {
        Memo1->Lines->Add("Ошибка: k больше или равно количеству слов.");
        return;
    }

    // Удаляем первые k слов
    words.erase(words.begin(), words.begin() + k);

    // Собираем оставшиеся слова в строку
    std::string result;
    for (size_t i = 0; i < words.size(); ++i) {
        result += words[i];
        if (i != words.size() - 1) {
            result += " ";  // Добавляем пробел между словами
        }
    }

    // Выводим результат в Memo1
    Memo1->Lines->Add("Результат: " + String(result.c_str()));
}

6 practice lab 

2 вариант

Список товаров, имеющихся на складе, включает в себя наименование
товара, количество единиц товара, цену единицы и дату поступления товара на
склад. Вывести в алфавитном порядке список товаров, хранящихся больше
месяца, стоимость которых превышает 10 000 р.

#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
#include <System.DateUtils.hpp> // Для работы с датами
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;

// Структура для хранения информации о товаре
typedef struct {
    AnsiString name;    // Наименование товара
    int quantity;       // Количество единиц товара
    double unitPrice;   // Цена за единицу товара
    TDateTime entryDate; // Дата поступления товара на склад
} TProduct;

TProduct products[100]; // Массив товаров
int productCount = 0;    // Количество товаров в массиве

__fastcall TForm1::TForm1(TComponent* Owner)
    : TForm(Owner)
{
}

// Функция для добавления товара в список
void __fastcall TForm1::AddProduct(AnsiString name, int quantity, double unitPrice, TDateTime entryDate)
{
    if (productCount < 100) {
        products[productCount].name = name;
        products[productCount].quantity = quantity;
        products[productCount].unitPrice = unitPrice;
        products[productCount].entryDate = entryDate;
        productCount++;
    }
}

// Функция для фильтрации и сортировки товаров
void __fastcall TForm1::FilterAndSortProducts()
{
    // Массив для отфильтрованных товаров
    TProduct filteredProducts[100];
    int filteredCount = 0;

    TDateTime currentDate = Now(); // Текущая дата

    // Фильтрация товаров: хранятся больше месяца и стоимость больше 10,000
    for (int i = 0; i < productCount; i++) {
        // Проверяем, что товар хранится больше месяца и его стоимость > 10,000
        if (DaysBetween(products[i].entryDate, currentDate) > 30 && products[i].unitPrice * products[i].quantity > 10000) {
            filteredProducts[filteredCount] = products[i];
            filteredCount++;
        }
    }

    // Сортировка отфильтрованных товаров по наименованию (алфавитно)
    for (int i = 0; i < filteredCount - 1; i++) {
        for (int j = i + 1; j < filteredCount; j++) {
            if (filteredProducts[i].name > filteredProducts[j].name) {
                TProduct temp = filteredProducts[i];
                filteredProducts[i] = filteredProducts[j];
                filteredProducts[j] = temp;
            }
        }
    }

    // Вывод отсортированных товаров в Memo1
    Memo1->Clear();
    for (int i = 0; i < filteredCount; i++) {
        Memo1->Lines->Add(filteredProducts[i].name + " " + IntToStr(filteredProducts[i].quantity) + " " + 
                          FloatToStr(filteredProducts[i].unitPrice) + " " + DateToStr(filteredProducts[i].entryDate));
    }
}

// Обработчик кнопки для добавления товара
void __fastcall TForm1::BtnAddProductClick(TObject *Sender)
{
    AnsiString name = EditName->Text;
    int quantity = StrToInt(EditQuantity->Text);
    double unitPrice = StrToFloat(EditUnitPrice->Text);
    TDateTime entryDate = DateEditEntryDate->Date;

    // Добавляем товар
    AddProduct(name, quantity, unitPrice, entryDate);

    // Очищаем поля ввода
    EditName->Clear();
    EditQuantity->Clear();
    EditUnitPrice->Clear();
}

// Обработчик кнопки для фильтрации и сортировки
void __fastcall TForm1::BtnFilterSortClick(TObject *Sender)
{
    FilterAndSortProducts();
}

17 и 18  вариант 

17. В исполкоме формируется список нуждающихся в улучшении
жилищных условий. Каждая запись этого списка содержит: порядковый номер,
Ф.И.О., величину жилплощади на одного члена семьи и дату постановки на учет.
Исходя из заданного количества квартир, выделяемых ежегодно, вывести весь
список с указанием ожидаемого года получения квартиры.
18. Имеется список женихов и список невест. Каждая запись списка
содержит пол, имя, возраст, рост, вес, а также требования к партнеру:
наименьший и наибольший возраст, наименьший и наибольший вес, наименьший
и наибольший рост. Объединить эти списки в список пар с учетом требований к
партнерам без повторений.


#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
#include <System.DateUtils.hpp> // Для работы с датами
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;

// Структура для хранения информации о человеке
typedef struct {
    int number;                 // Порядковый номер
    AnsiString name;            // Ф.И.О.
    double livingSpace;         // Жилплощадь на одного члена семьи
    TDateTime registrationDate; // Дата постановки на учет
    int yearsToWait;            // Годы ожидания квартиры
    int expectedYear;           // Ожидаемый год получения квартиры
} TPerson;

TPerson people[100]; // Массив людей
int personCount = 0;  // Количество людей в списке

// Функция для добавления человека в список
void __fastcall TForm1::AddPerson(int number, AnsiString name, double livingSpace, TDateTime registrationDate, int apartmentsPerYear)
{
    if (personCount < 100) {
        people[personCount].number = number;
        people[personCount].name = name;
        people[personCount].livingSpace = livingSpace;
        people[personCount].registrationDate = registrationDate;

        // Рассчитываем количество лет ожидания
        int yearsWaiting = personCount / apartmentsPerYear;
        people[personCount].yearsToWait = yearsWaiting;
        people[personCount].expectedYear = YearOf(Now()) + yearsWaiting;
        
        personCount++;
    }
}

// Функция для вывода списка с ожидаемыми годами
void __fastcall TForm1::ShowList()
{
    Memo1->Clear();
    for (int i = 0; i < personCount; i++) {
        Memo1->Lines->Add("№" + IntToStr(people[i].number) + " " + people[i].name + 
                          " Жилплощадь на одного члена семьи: " + FloatToStr(people[i].livingSpace) + 
                          " Ожидаемый год получения квартиры: " + IntToStr(people[i].expectedYear));
    }
}

18 вариант 

#include <vcl.h>
#pragma hdrstop
#include "Unit1.h"
#pragma package(smart_init)
#pragma resource "*.dfm"
TForm1 *Form1;

// Структура для хранения информации о человеке (женихе или невесте)
typedef struct {
    AnsiString gender;         // Пол (жених/невеста)
    AnsiString name;           // Имя
    int age;                   // Возраст
    double height;             // Рост
    double weight;             // Вес
    int minAge, maxAge;        // Требования к возрасту партнера
    double minHeight, maxHeight; // Требования к росту партнера
    double minWeight, maxWeight; // Требования к весу партнера
} TPerson;

TPerson grooms[100], brides[100]; // Списки женихов и невест
int groomCount = 0, brideCount = 0; // Количество женихов и невест

// Функция для добавления жениха или невесты
void __fastcall TForm1::AddPersonToList(AnsiString gender, AnsiString name, int age, double height, double weight, 
                                          int minAge, int maxAge, double minHeight, double maxHeight, double minWeight, double maxWeight)
{
    if (gender == "Groom") {
        grooms[groomCount].gender = gender;
        grooms[groomCount].name = name;
        grooms[groomCount].age = age;
        grooms[groomCount].height = height;
        grooms[groomCount].weight = weight;
        grooms[groomCount].minAge = minAge;
        grooms[groomCount].maxAge = maxAge;
        grooms[groomCount].minHeight = minHeight;
        grooms[groomCount].maxHeight = maxHeight;
        grooms[groomCount].minWeight = minWeight;
        grooms[groomCount].maxWeight = maxWeight;
        groomCount++;
    } else if (gender == "Bride") {
        brides[brideCount].gender = gender;
        brides[brideCount].name = name;
        brides[brideCount].age = age;
        brides[brideCount].height = height;
        brides[brideCount].weight = weight;
        brides[brideCount].minAge = minAge;
        brides[brideCount].maxAge = maxAge;
        brides[brideCount].minHeight = minHeight;
        brides[brideCount].maxHeight = maxHeight;
        brides[brideCount].minWeight = minWeight;
        brides[brideCount].maxWeight = maxWeight;
        brideCount++;
    }
}

// Функция для создания списка пар
void __fastcall TForm1::CreatePairs()
{
    Memo1->Clear();
    for (int i = 0; i < groomCount; i++) {
        for (int j = 0; j < brideCount; j++) {
            if (grooms[i].age >= brides[j].minAge && grooms[i].age <= brides[j].maxAge &&
                grooms[i].height >= brides[j].minHeight && grooms[i].height <= brides[j].maxHeight &&
                grooms[i].weight >= brides[j].minWeight && grooms[i].weight <= brides[j].maxWeight) {
                Memo1->Lines->Add(grooms[i].name + " and " + brides[j].name);
            }
        }
    }
}


9 practice 

2 вариант 

Перевод числа из троичной системы счисления в четырнадцатеричную

#include <iostream>
#include <cmath>
#include <string>
using namespace std;

// Функция для перевода из троичной системы в десятичную
int TernaryToDecimal(string ternary) {
    int decimal = 0;
    int power = 0;
    for (int i = ternary.length() - 1; i >= 0; i--) {
        decimal += (ternary[i] - '0') * pow(3, power);
        power++;
    }
    return decimal;
}

// Функция для перевода из десятичной системы в четырнадцатеричную
string DecimalToHexadecimal(int decimal) {
    if (decimal == 0) return "0";
    string hexadecimal = "";
    while (decimal > 0) {
        int remainder = decimal % 14;
        if (remainder < 10)
            hexadecimal = (char)(remainder + '0') + hexadecimal;
        else
            hexadecimal = (char)(remainder - 10 + 'A') + hexadecimal;
        decimal /= 14;
    }
    return hexadecimal;
}

int main() {
    string ternary;
    cout << "Enter a number in ternary system: ";
    cin >> ternary;

    // Перевод из троичной в десятичную
    int decimal = TernaryToDecimal(ternary);
    cout << "Decimal equivalent: " << decimal << endl;

    // Перевод из десятичной в четырнадцатеричную
    string hexadecimal = DecimalToHexadecimal(decimal);
    cout << "Hexadecimal equivalent: " << hexadecimal << endl;

    return 0;
}

17. В десятичной и четверичной системах счисления

#include <iostream>
#include <cmath>
#include <string>
using namespace std;

// Функция для перевода из десятичной системы в четверичную
string DecimalToQuaternary(int decimal) {
    if (decimal == 0) return "0";
    string quaternary = "";
    while (decimal > 0) {
        int remainder = decimal % 4;
        quaternary = (char)(remainder + '0') + quaternary;
        decimal /= 4;
    }
    return quaternary;
}

// Функция для перевода из четверичной системы в десятичную
int QuaternaryToDecimal(string quaternary) {
    int decimal = 0;
    int power = 0;
    for (int i = quaternary.length() - 1; i >= 0; i--) {
        decimal += (quaternary[i] - '0') * pow(4, power);
        power++;
    }
    return decimal;
}

int main() {
    int decimal;
    string quaternary;

    // Перевод из десятичной в четверичную
    cout << "Enter a number in decimal system: ";
    cin >> decimal;
    cout << "In quaternary system: " << DecimalToQuaternary(decimal) << endl;

    // Перевод из четверичной в десятичную
    cout << "Enter a number in quaternary system: ";
    cin >> quaternary;
    cout << "In decimal system: " << QuaternaryToDecimal(quaternary) << endl;

    return 0;
}

