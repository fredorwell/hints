# Шпаргалка по Python

## Типы данных 
### Integer - Целые числа - `int(var)` - Пример: 65
### float - с плавающей точкой (вещественные)  - `float(var)` - Пример: 12.05
### bool - логические  - `bool(var)` - Возможные значения: True, False
### str - Строка  - `str(var)` - 'asd123456'
#### Полезные методы со строками
- складывание
```
 srt1 = 'asd'
 str2 = 'zxc'
 str3 = srt1 + srt2 => 'asdzxc'
```
- Срез - `str[start:stop:step]`
```
str = 'qwertyuiop'
print(str[0:5]) => qwert - с первого по пятый элемент
print(str[::-1]) => poiuytrewq - с шагом в минус один
```
- Поиск подстроки - метод `.find('иском знач')` вернет индекс на котором находится искомая подстрока
```
str1 = 'qwertypusu'
print(str1.find('rty')) => 3
```
- Замена подстроки - метод `.replace('иском знач', 'новое знач')` заменит в строке `искомое значение` на `новое знач`
```
str1 = 'qwertypusu'
print(str1.replace('qwe','ewq')) => ewqrtypusu
```
- Разделение на элементы списка - метод `.split('разделитель')` разобьет строку на элементы списка
```
str1 = 'qwe qwe qwe'
print(str1) => qwe qwe qwe
print(str1.split(' ')) => ['qwe', 'qwe', 'qwe']
```
- Строка иттерируемый объект и по нему можно идти циклом `for`
```
str1 = 'qwer'
for i in str1:
    print(i)
Result:
q
w
e
r
```

### list - список или массив - Пример: `['a', 'b', 1, '2']`
Элементом списка может быть что угодно начиная от строки, заканчивая другим списком или списком списков.
#### Полезные методы со списками
- Добавление нового элемента - Делается с помощью метода `.append('элемент')`
```
my_list = [1, 2, 3, 4]
my_list.append(5)
print(my_list) => [1, 2, 3, 4, 5]
```
- Удаление элемента по индексу - делается с помощью метода `.pop('индекс элемента')`
```
my_list = [1, 2, 3, 4]
my_list.pop(0)
print(my_list) => [2, 3, 4]
```
- Сортировка списка - делается с помощью метода `.sort()`
```
my_list = [2, 1, 5, 3, 4]
my_list.sort()
print(my_list) => [1, 2, 3, 4, 5]
```
- __!Важный момент при обработке списков!__
```
Если мы идем по массиву через for i in my_list, то мы можем делать что угодно, но не изменять список, т.е. чтение/вывод/сравнение и т.п. Если мы попытаемся как в примере ниже поменять каждый элемент списка на 1, то у нас ничего не получится.
my_list = [2, 1, 5, 3, 4]
for i in my_list:
    i = 1
print(my_list) => [2, 1, 5, 3, 4]

Для изменения массива нам надо задавать условие for через range
my_list = [2, 1, 5, 3, 4]
for i in range(len(my_list)):
    my_list[i] = 1
print(my_list) => [1, 1, 1, 1, 1]

```
### dict - словарь - это коллекция из пар `'Ключ':'Значение'`
- Обращение к элементу - `название словаря ['Ключ']`
```
Пример:
my_dict = {'pow': 2, 'value': 12, 'equ': 300}
print(f'{my_dict["value"]}x**{my_dict["pow"]} = {my_dict["equ"]}')
=> 12x**2 = 300
```
- Добавление элемента и перезапись - `название словаря ['новый ключ']` и если такого ключа нет, то мы добавим, однако если он присутсвует, то мы перезапишем
```
Пример:
my_dict = {'pow': 2, 'value': 12, 'equ': 300}
my_dict['new_key'] = 88
print(my_dict) => {'pow': 2, 'value': 12, 'equ': 300, 'new_key': 88}
my_dict['new_key'] = 16
print(my_dict) => {'pow': 2, 'value': 12, 'equ': 300, 'new_key': 16}
```
- Удаление ключа и значения - `del название словаря ['ключ']`
```
Пример:
my_dict = {'pow': 2, 'value': 12, 'equ': 300, 'new_key': 88}
del my_dict['new_key']
print(my_dict) => {'pow': 2, 'value': 12, 'equ': 300}
```
### tuple - Кортеж - это список корторый нельзя изменить 
```
my_tuple = tuple('12345678')
print(my_tuple) => ('1', '2', '3', '4', '5', '6', '7', '8')
```
### set - множество - это список УНИКАЛЬНЫХ элементов 
```
Если друг мы попытаемся создать множество с неуникальными элементами, то эти значения удалятся из него
my_list = [1, 2, 3, 4, 5, 5, 5, 6]
print(my_list) => [1, 2, 3, 4, 5, 5, 5, 6]
my_list = set(my_list)
print(my_list) => {1, 2, 3, 4, 5, 6}
Очень удобно если надо убрать из списка дубликаты
```
## ввод/вывод в консоль
### Ввод данных
Ввод данных осуществляется с помощью комманды `input('Текст для ввода')`, изначально все что принимает консоль - это строка.
```
a = input('Введите значение') => Введите значение: asd
print(a) => asd
```
### Вывод данных
Вывод делаем через комманду `print(выводимое значение)`, однако если мы хотим вывести текст и значение переменной, то делаем интерполяцию через f-строку
```
a = 'asdasdasd'
print(a[0:3]) => asd
print(f'Срез строки: {a[0:3]} ') => Срез строки: asd 
```
## Ветвление
У ветвления есть три основных момента if, elif, else
```
a = -1

if 0 < a < 50:
    print('Значение больше нуля, но меньше 50')
elif a < 0:
    print('Значение меньше нуля') =Ю Значение меньше нуля
else:
    print('Значение Больше 50')
```
Есть опция с тернарным операторами
```
a = 10
print('Значение меньше нуля') if a < 0 else print('Значение больше нуля') => Значение больше нуля
```
## Перехват исключений
Конструкция try - except очень полезная если нам нужно отловить исключения
```
a = input('Введите значение: ') => Введите значение: фыв
try:
    a = int(a)
    print('Вы ввели число')
except:
    print('Вы ввели строку') => Вы ввели строку
```

## Циклы
### for - цикл идет от i до любого значения, либо можем идти напрямую по итерируемым объектам (списки, строки и т.п.)
```
В цикле можно идти по индексам от 0 до максимального значения массива:
my_list = [1, 2, 3, 4]
for i in range(len(my_list)):
    print(f'Элемент с индексом {i} - {my_list[i]}')

result:
Элемент с индексом 0 - 1
Элемент с индексом 1 - 2
Элемент с индексом 2 - 3
Элемент с индексом 3 - 4
В данном случае мы можем изменять элементы массива и имеем доступы к их индексам

Либо по самим элементам(В таком случае нельзя их изменять):
my_list = [1, 2, 3, 4]
for i in my_list:
    print(f'Элемент - {i}')

result:
Элемент - 1
Элемент - 2
Элемент - 3
Элемент - 4

В таком случае мы теряем индексы элементов и не можем их менять, но очень удобно сравнивать/выводить, обарабатывать и т.п.

```
### while - цикл выполняется пока условие истинное
```
Пример самой простой конструкции 
a = 1
while a < 1000:
    a *= 10
    print(a)

Result:
10
100
1000

Однако с помощью break можно прирывать цикл в любой момент
a = 1
while True:
    a *= 10
    if a > 1000:
        break
print(a)

Result:
10000
```

## ф-ции
Функции пишутся в начале файла 
```
Пример функции деления на пополам
def Half(value: int):
    value /= 2
    return value


a = 1000
print(Half(a)) => 500.0
```
Существуют лямбда функции, по сути это просто упрощение записи ф-ции для самых простых операций
```
Пример функции деления на пополам в формате лямбда-функции
Half = lambda x, y: x / y
a = Half(1000, 2)
print(a)
```

## Импорт ф-ций

Основная конструкция для импорта это - `from 'Название библиотеки' import 'название метода' as 'алиас'`
```
from random import randint as rnd

a = rnd(1,10)
print(a)
```

## Работа с файлами
### Основные методы
- f = `open(Путь, 'режим открытия', encoding='UTF-8')` - открывает файл для чтения 
- `.close()` - закрывает файл
- `.read(n)` - Читает n элементов файла
- `.readline()` - читает одну строку
- `.readlines()` - вертает список всех строк в файле
- `.write(str)` - добавляет строку `str` в файл
- `.writelines(str)` - добавляет последовательность строк в файл
```
Пример базовой логики работы с файлом:
path = 'test.txt' -> указали путь
file = open(path, 'r', encoding='UTF-8') -> Открыли файл
data = file.read() -> Прочитали
file.close() -> Закрыли файл
print(data) -> вывели данные из файла: Тут написано что ты молодец

Но это метод для лохов, надо делать так:
path = 'test.txt'

with open(path, 'r', encoding='UTF-8') as file:
    print(file.read())

Поскольку конструкция with open и открывает и закрывает файл нет вероятности забыть его закрыть. 
```
### Режимы открытия файла
 - r - Чтение файла
 - a - Добавление строк в файл - создаст если не найдет
 - w - Запись в файл - создаст файл если не найдет + __перезапишет его!__
 - r+ - Чтение и запись

## Установка сторонних библиотек
Для установки сторонней библиотеки зайди в консоль и введи комманду `pip install название бибилотеки`

__ОЧЕНЬ ВАЖНО__
Если ты работаешь через вирт машину, то ставь библиотеку в `/venv/scripts`.

После просто сделай вызов скачанной библиотеки через `import`

### Полезные команды
- pip help - вызов хелпа
- pip install - Установка пакета
- pip uninstall - Удаление пакета
- pip search - поиск пакета по имени
- pip install -U - обновление пакета
- pip install --force-reinstall - форс обновление пакета

Примечание: Если ты опустился до установки библиотек из интернета ищи их тут https://pypi.org/

