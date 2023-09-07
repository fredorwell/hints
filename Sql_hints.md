# Шпаргалка по SQL

## Создание, удаление и изменение таблиц

### Создание таблицы
<pre>
CREATE TABLE `db_name`.`table_name` (
  `column1` INT ZEROFILL NOT NULL AUTO_INCREMENT PRIMARY KEY PRIMARY KEY,
  `column2` VARCHAR(45) NOT NULL,
  `column3` VARCHAR(45) NOT NULL,
  `column4` INT NULL);
</pre>

Возможные параметры:
- type - тип данных в колонке (Основные: INT, VARCHAR(N), DATE, TIMESTAMP );
- ZEROFILL - в случае если поле будет не заполненным, т.е. null, то присвоится 0;
- NOT NULL - Поле не должно содержать null;
- AUTO_INCREMENT - автоинкиментируемость столбца;
- PRIMARY KEY - первичный ключ для таблицы;

### Создание таблицы
Удаление производим с помощью ключевого слова `drop table`, синтаксис ниже:
<pre>
drop table `db_name`.`table_name`;
</pre>

### изменение таблицы
Удаление производим с помощью ключевого слова `alter table`, синтаксис ниже:
<pre>
drop table `db_name`.`table_name`;
</pre>

## Добавление, изменение, удаление данных в таблице
### Добавление данных
Добавление данных в таблицу происходит через ключевое слово `INSERT INTO`, Ниже описан синтаксис:
<pre>
INSERT INTO `db_name`.`table_name` (`column2`, `column3`, `column4`) VALUES ('value_column2_1', 'value_column3_1', 'value_column4_1'),
('value_column2_2', 'value_column3_2', 'value_column4_2'),
('value_column2_3', 'value_column3_3', 'value_column4_3'),
;
</pre>

- db_name - название бд к которой обращаемся;
- table_name - название таблицы к которой обращаемся;
- (`column2`, `column3`) - Список колонок в которую мы планируем записывать данные;
- (`value_column2`, `value_column3`) - Список значений которые мы планируем внести;

### Изменение данных
Изменение данных в таблице происходит через ключевое слово `UPDATE`, Ниже описан синтаксис:

<pre>
update table_name set column3 = column3 + 5, column4 = 'changed' where column2 = 'condition';
</pre>
В данном мы изменили значения в column3 (увеличили его на 5) и заменили значение column4 на changed для тех полей которые подходят под условие `condition`.
> Прим: Если sql ругается что ты в safe mode, то необходимо его отключить `SET SQL_SAFE_UPDATES = 0;`
>>НЕ ВЗДУМАЙ ЭТО ДЕЛАТЬ НА ПРОДЕ!

### Удаление данных
Удалить строку в таблице можно с помощью ключевого слова `DELETE`
<pre>
delete from table_name where column2 = 'delete_value';
</pre>


## Выборка, фильтрация, сортировка и агрегация
### Выборка
Вывести данные из таблицы можно с помощью ключевого слова `select`:
<pre>
select column1, column2 from table_name where [filter];
</pre>
- column1, column2 OR * - Столбцы которые нам необходимо вывести;
- from table_name - из какой таблицы;
- where [filter] - фильтрация по условию

### Выборка
Фильтрация происходит через ключевое слово `where` где и происходят основные танцы с бубном поскольку в фильтр можно встроить логическую операцию, подзапрос, if, case и все что только душе угодно.
#### Базовые фильтрации
В фильтрации можно использовать арифм. операции
<pre>
select * from table_name where column3 = 42; - Равенство
select * from table_name where column3 != 42; - отрицание
select * from table_name where NOT column3 = 42; - тоже отрицание
select * from table_name where column3 > 42; - Больше
select * from table_name where column3 < 42; - Меньше
select * from table_name where column3 <= 42; - Меньше или равно
</pre>
И так же можно использовать регулярные выражения c ключевым словом:
- % - любое кол-во символов
- _ - любой один символ
- [a-f] - Один любой символ в диапазоне [a-f] или например [abcdef]
Прим: Это работает только с REGEXP и я хз почему, но вот так.

<pre>
select * from table_name where column3 LIKE 'a%'; - начинаются с 'a'
select * from table_name where column3 LIKE '%a'; - заканчиваются на 'a'
select * from table_name where column3 LIKE '_a_'; - всего 3 буквы, посередине 'а'
select * from table_name where column3 regexp '[0-9]'; - Присутсвует любая цифра
</pre>

#### Логические операции в фильтрации
В фильтрации можно использовать такие логические операции как `AND`, `OR`, `NOT` и еще тьму тьмущую разных штук, полный список смотри в ссылке внизу доки

<pre>
select * from table_name where NOT(column3 regexp '[0-9]') OR (column3 like 'a%');
Любые значения которые содержат цифру или начинаются на 'а'
select * from table_name where (column3 regexp '[0-9]') and NOT (column3 like 'a%');
Любые значения которые содержат цифру и не начинаются на 'а'
</pre>

#### Конструкция IN
Можно так же фильтровать по списку или набору данных с помощью ключевого слова `IN`
<pre>
select * from table_name where column3 [NOT] in (value_condition1, value_condition2);
-- в данном случае мы фильтруем значения по наличию их среди значений в таблице

select * from table_name1 where column1 [NOT] in (select column1 from table_name2);
-- В данном случае мы отбираем строки в table_name1 у которых в column1 значение находится внутри результирующей таблицы (select column1 from table_name2)

</pre>
> Прим: Так же в выражение можно встроить подзапрос и фильтровать по результатам подзапроса.

#### Конструкция exists
exists нам вернет true или false и его мы можем использовать в качестве проверки на какое-то условие

<pre>
select *
from table_name1
where [not] exists (select * from table_name2 where table_name1.column1 = table_name2.column2);
</pre>



#### Конструкция CASE
Можно использовать конструкцию `case`, для дашбордов полезно
<pre>
select column1, column2, 
case
	when column3 = state1
		then 'value_state1'
	when column3 = state2
		then 'value_state2'
	when column3 >= state3
		then 'value_state3'
	else 'value_stateElse'
END as name_new_column
from table_name;
</pre>


#### Конструкция IF
<pre>
select column1, column2, IF(condition, value_true, value_false) as name_new_column
from table_name;
</pre>


#### Сортировка
Сортировать можно с помощью добавления `ORDER BY`, пример запроса ниже:
<pre>
select * from table_name [where condition] order by column2 [asc|desc];
</pre>
asc - по возрастанию
desc - по убыванию

#### Лимитирование выборки
Лимитирование выборки происходит в разных субд с помощью разных ключевых слов:
- TOP - ms access, sql server
- LIMIT - MySql, PostgreSql, SQLite
- FETCH FIRST - Oracle

<pre>
select * from table_name 
[where condition] 
LIMIT [qty_skip_row] qty_view_row;
Выводим все столбцы для записей начиная со строки qty_skip_row+1, всего записей qty_view_row
</pre>
> Прим: у меня стоит только mysql по этому и пример делаю по нему

#### Уникализация выборки
Вывести только уникальные значения можно с помощью ключевого слова `Distinct`

<pre>
select distinct column1 from table_name [where condition];
Выводим только уникальные значения столбца column1 удовлетворяющие условиям.
</pre>

#### Групировка
Групировка записей происходит с помощью ключевого слова `group by`, формирует группы по уникальным значениям указанного столбца, ниже синтаксис:
<pre>
select column1, [aggregate_function]
from table_name
[where conition_for_rows]
[group by column1]
[having conition_for_filter_group]
[order by column_for_sorting];
</pre>

#### Агрегатные ф-ции
в mysql есть следующие агрегатные ф-ции:
- AVG - среднее значение
- SUM - сумма значений
- MIN - Минимальное значение
- MAX - Максимальное значение
- COUNT - количество строк взапросе

<pre>
select column1,
[AVG(column2)],
[SUM(column2)],
[MIN(column2)],
[MAX(column2)],
from table_name;
</pre>


## UNION, JOIN, подзапросы
### Union
С помощью ключевого слова `UNION` можно объеденить два или более селекта в одну резуьтирующую таблицу удалив повторяющиеся значения, синтаксис ниже:

<pre>
select column1, column2 from table1_name
UNION
select column3, column4 from table2_name;
</pre>
> Прим: с помощью UNION можно соединять абсолютно любые столбцы, но количество столбцов должно быть всегда одинаковое

>Так же есть дополнительный вариант UNION - это UNION ALL. Он не удаляет повторяющиеся строки.

### JOIN
Join объеденяет таблицы по ключу, основные виды:
- `[inner]` join - Пересечение таблиц - дефолтный вариант
- left `[outer]` join - Присоединение к левой таблице
- right `[outer]` join - Присоединение к правой таблице
- full join - обе таблицы + их пересесечение
- cross join - декартово произведение таблиц


<img src="https://www.thoughtco.com/thmb/xh4MUu8HQyX1JVEcxn2IorWogoo=/1500x0/filters:no_upscale():max_bytes(150000):strip_icc()/0iHiL-d7a0c49a861448cb94477386a6f3f05b.png" title="виды join" width="500" />

#### Пример использования inner join или просто join:
<pre>
select 
table_name1.column_name, - Поле из первой таблицы
table_name2.column_name, - Поле из второй таблицы
(table_name2.column_name * table_name2.column_name) as operation - Пример операций между таблицами
from table_name1 [as table1]- Правая таблица
[inner] join table_name2 [as table2] - Левая таблица
ON table_name1.column_name = table_name2.column_name;  - по какому ключу объединяем
</pre>
> Прим: В примере указано обращение к колонкам с указанием названия таблицы имхо очень полезная штука.

#### Пример использования outer join left|right:

<pre>
select 
table_name1.column_name, - Поле из левой таблицы
table_name2.column_name - Поле из правой таблицы
from table_name1
[right|left] [outer] join table_name2 
ON table_name1.column_name = table_name2.column_name; 
</pre>
> Прим: писать outer join не обязательно, синтаксис у левого и правого похож.

#### Пример использования full join:
В mysql нет фулл джоина и я в целом понимаю почему, но если прям очень нужно его сделать, то надо костылить с помощью левого + правого джойнов, пример ниже:

<pre>
select 
table_name1.column_name, - Поле из левой таблицы
table_name2.column_name - Поле из правой таблицы
from table_name1
left outer join table_name2 
ON table_name1.column_name = table_name2.column_name
-- левый джоин
union

select 
table_name1.column_name, - Поле из левой таблицы
table_name2.column_name - Поле из правой таблицы
from orders
right outer join products 
ON table_name1.column_name = table_name2.column_name; 
-- правый джоин
</pre>

#### Пример использования cross join:
Как же низко ты пал раз тебе понадобился этот вид джоина, но ладно. Этот джоин по факту объединяет каждую строку левой таблицы со всеми строками в правой таблицы, что выглядит как декартово произведение. 

<pre>
select *
from table_name1
cross join table_name2; 
</pre>




## Оконные функции

## Временные таблицы


# Полезные ссылки
- https://habr.com/ru/articles/564390/
- https://learn.microsoft.com/en-us/sql/t-sql/language-elements/operators-transact-sql