## Шпаргалка по C#

### Консольные комманды
- dotnet new console - Создание нового проекта
- dotnet run - Запускает текущий проект

### Комманды

- Console.Write("`текст`"); - Сообщение для вывода `текста` в консоли
- Console.WriteLine("`текст`"); - Сообщение для вывода `текста` в консоли с переносом строки
- Console.ReadLine(); - Запись в переменную значения;
- new Random().Next(`min`,`max`); - Рандомайзер чисел от `min` до `max`

### Основные конструкции
#### Ветвление
```
if (Условие)
{
	Набор действий истина
}
else
{
	Набор действий ложь	
}

Пример:
int a = 5;
int b = 3;
if (a + b > 10)
    Console.WriteLine("The answer is greater than 10");
else
    Console.WriteLine("The answer is not greater than 10");
```
#### Цикл While
```
while (Условие продолжения)
{
	Набор действий
}

Пример:
int counter = 0;
while (counter < 10)
{
    Console.WriteLine($"Hello World! The counter is {counter}");
    counter++;
}
```
#### Цикл for
```
for (Начальное значение счетчика; Условие выхода; иттератор)
{
    Набор действий
}

Пример:
for (int index = 0; index < 10; index++)
{
    Console.WriteLine($"Hello World! The index is {index}");
}
```
Типы данных
int - integer
double - иррациональные
srting - строки
bool - логический