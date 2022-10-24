# Шпаргалка по C#

## Консольные комманды
- dotnet new console - Создание нового проекта
- dotnet run - Запускает текущий проект

## Комманды

- Console.Write("`текст`"); - Сообщение для вывода `текста` в консоли
- Console.WriteLine("`текст`"); - Сообщение для вывода `текста` в консоли с переносом строки
- Console.ReadLine(); - Запись в переменную значения;
- new Random().Next(`min`,`max`); - Рандомайзер чисел от `min` до `max`
- `переменная` = Convert.ToInt32(Console.ReadLine()); - Конвертирует стринг в инт

## Основные конструкции
### Массивы
Объявление массива
Синтаксис
```
тип_переменной[] название_массива; - одномерные массивы
тип_переменной[,] название_массива; - двумерные массивы
```
Пример:
```
// Объявление массива с значениями {0, 0, 0, 0}
int[] nums = new int[4];

// Объявление массива с значениями {1, 2, 3, 4}
int[] nums = {1, 2, 3, 4};

// объявление массива с значениями {15, 1211, 433, 54}
int[] array = {15, 1211, 433, 54};
//Индексы       0    1    2   3
```
### Операции с массивами
- int lenthg = array.Length - Запись в переменную `lenthg` длинну массива `array`
### Ветвление `if`
Синтаксис:
```
if (Условие)
{
	Набор действий истина
}
else
{
	Набор действий ложь	
}
```
Пример:
```
// Нахождение максимума среди двух чисел (Прим: Без возможности равенства двух чисел)
int num1 = 8;
int num2 = 6;
if(num1 > num2)
{
    Console.WriteLine($"Число {num1} больше числа {num2}");
}
else
{
    Console.WriteLine($"Число {num1} меньше числа {num2}");
}
```
### Модификатор ветвление `else if`
Синтаксис:
```
if (Условие1)
{
	Набор действий если условие1 == истина
}
else if (Условие2)
{
	Набор действий если условие2 == истина
}
else if (Условие3)
{
	Набор действий если условие3 == истина
}
else
{
    Набор действий условие3 == ложь 
}
```
Пример:
```
// Сравнение двух чисел
int num1 = 8;
int num2 = 6;
if(num1 > num2)
{
    Console.WriteLine($"Число {num1} больше числа {num2}");
}
else if (num1 < num2)
{
    Console.WriteLine($"Число {num1} меньше числа {num2}");
}
else
{
    Console.WriteLine("Число num1 равно числу num2");
}
```
### Конструкция `switch`
Синтаксис:
```
switch (выражение)
{
    case значение1:
        код,выполняемый если выражение имеет значение1
        break;
    case значение2:
        код,выполняемый если выражение имеет значение2
        break;
    case значение3:
        код, выполняемый если выражение имеет значение3
        break;
    default:
        код, выполняемый если выражение не имеет ни одно из выше указанных значений
        break;
}
```
Пример:
```
string name = "Alex";
 
switch (name)
{
    case "Bob":
        Console.WriteLine("Ваше имя - Bob");
        break;
    case "Tom":
        Console.WriteLine("Ваше имя - Tom");
        break;
    case "Sam":
        Console.WriteLine("Ваше имя - Sam");
        break;
    default:
        Console.WriteLine("Неизвестное имя");
        break;
}
```
#### ***Очень важное примечание:***
```
В конце каждого блока сase должен ставиться один из операторов перехода: break, goto case, return или throw. Как правило, используется оператор break. При его применении другие блоки case выполняться не будут.
```

## Циклы
### Цикл `While`
Синтаксис:
```
while (Условие продолжения)
{
	Набор действий
}
```
Пример:
```
int counter = 0;
while (counter < 10)
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
}
```
### Цикл `for`
Синтаксис:
```
for (Начальное значение счетчика; Условие выхода; иттератор)
{
    Набор действий
}
```
Пример:
```
for (int index = 0; index < 10; index++)
{
    Console.WriteLine($"Hello World! The index is {index}");
}
```
## Методы (Функции)

### `Void метод`
Void методы - это функции которые не отдают на выход какое либо значение, например вывод массива или заполнение массива случайными числами.
Синтаксис:
```
void *название_метода*(аргумент)
{
    Тело метода
}
```
Пример void метода (ф-ции) по заполнению массива случайными значениями:
```
void FillArray(int[] collection)
{
    int length = collection.Length;
    int index = 0;
    while (index < length)
    {
        collection[index] = new Random().Next(1, 10);
        index++;
    }

}
```
Пример void метода (ф-ции) по выводу массива в консоль:
```
void PrineArray(int[] collection)
{
    int length = collection.Length;
    int index = 0;
    while (index < length)
    {
        Console.Write($"{collection[index]} ");
        index++;
    }
}
```
Пример void метода (ф-ции) по выводу двумерного массива в консоль:
```
void PrintMatrix(int[,] matrix)
{
    for (int i = 0; i < matrix.GetLength(0); i++)
    {
        Console.Write("|");
        for (int j = 0; j < matrix.GetLength(1); j++)
        {
            if (j < matrix.GetLength(1) - 1) Console.Write($"{matrix[i, j], 4} | ");
            else Console.Write($"{matrix[i, j], 4} ");
        }
        Console.WriteLine("|");
    }
}
```

### `Метод с возвратом значения`
Синтаксис:
```
тип_возврата имя_метода(аргумент)
{
    Тело метода
    return *имя переменной которую необходимо отдать в результат*;
}
```
Пример метода по нахождению максимума из трех значений:
```
int fMax(int arg1, int arg2, int arg3)
{
    int result = arg1;
    if (arg2 > result) result = arg2;
    if (arg3 > result) result = arg3;
    return result;
}
```
Пример метода создающего и возвращающего массив:
```
int[] CreateArrayRndInt(int size, int min, int max)
{
    int[] array = new int[size];
    var rnd = new Random();
    for (int i = 0; i < array.Length; i++)
    {
        array[i] = rnd.Next(min, max + 1);
    }
    return array;
}
```
Пример метода создающего и возвращающего двумерный массив:
```
int[,] CreateMatrixRndInt(int rows, int columns, int min, int max)
{
    int[,] matrix = new int[rows, columns];
    var rnd = new Random();

    for (int i = 0; i < matrix.GetLength(0); i++) // 0 - rows  0 
    {
        for (int j = 0; j < matrix.GetLength(1); j++) // 1 - columns
        {
            matrix[i, j] = rnd.Next(min, max + 1);
        }
    }
    return matrix;
}
```
### Рекурсии
Примеры выполнения рекурсии можно найти в репозитории
https://github.com/fredorwell/eductation/tree/main/C%23/Lesson_9


Все выполненные работы по C# ты найдешь в репозитории
https://github.com/fredorwell/eductation/tree/main/C%23