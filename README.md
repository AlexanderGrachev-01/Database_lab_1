# Database_lab_1

:white_check_mark: **1. Дана схема базы данных в виде следующих отношений. С помощью операторов SQL создать логическую структуру соответствующих таблиц для хранения в СУБД, используя известные средства поддержания целостности (NOT NULL, UNIQUE, и т.д.). Обосновать выбор типов данных и используемые средства поддержания целостности. При выборе подходящих типов данных использовать информацию о конкретных значениях полей БД.**

```sql
CREATE TABLE "ЗАКАЗЧИК"
(
    "ИДЕНТИФИКАТОР" integer not null
        constraint заказчик_pk
            primary key,
    "ФАМИЛИЯ"       varchar not null,
    "РАЙОН"         varchar not null,
    "СКИДКА, %"     smallint
);

CREATE TABLE "ПУНКТ ПРОКАТА"
(
    "ИДЕНТИФИКАТОР"   integer not null
        constraint "пункт проката_pk"
            primary key,
    "НОМЕР"           varchar not null,
    "РАСПОЛОЖЕНИЕ"    varchar not null,
    "КОМИССИОННЫЕ, %" integer not null
);

CREATE TABLE "ВЕЩИ"
(
    "ИДЕНТИФИКАТОР"                 integer not null
        constraint вещи_pk
            primary key,
    "НАЗВАНИЕ"                      varchar not null,
    "СКЛАД"                         varchar not null,
    "КОЛ-ВО"                        integer not null,
    "ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ" integer not null
);

create table "ПРОКАТ"
(
    "НОМЕР"         integer not null
        constraint прокат_pk
            primary key,
    "КЛИЕНТ"        integer not null,
    "ДАТА"          varchar not null,
    "ПУНКТ ПРОКАТА" integer not null,
    "ВЕЩЬ"          integer not null,
    "СРОК ПРОКАТА"  integer not null,
    "СУММА, РУБ"    integer not null
);
```


:white_check_mark: **2. Ввести в ранее созданные таблицы конкретные данные (см. прил. 1). Использовать скрипт-файл из операторов INSERT или вспомогательную утилиту.**
```sql
INSERT INTO "ЗАКАЗЧИК"("ИДЕНТИФИКАТОР", "ФАМИЛИЯ", "РАЙОН", "СКИДКА, %")
 VALUES (001, 'Жалнин' ,'Приокский', 2),
        (002, 'Семенов' ,'Советский', 6),
        (003, 'Кожаков' ,'Ленинский', 0),
        (004, 'Шерстнев' ,'Автозаводский', 0),
        (005, 'Козлов' ,'Нижегородский', 4);

INSERT INTO "ПУНКТ ПРОКАТА"("ИДЕНТИФИКАТОР", "НОМЕР", "РАСПОЛОЖЕНИЕ", "КОМИССИОННЫЕ, %")
 VALUES (001, 'N23', 'Нижегородский', 4),
        (002, 'N16', 'Советский', 5),
        (003, 'N8', 'Сормовский', 7),
        (004, 'N21', 'Приокский', 3),
        (005, 'N12', 'Нижегородский', 2),
        (006, 'N6', 'Канавинский', 5);

INSERT INTO "ВЕЩИ"("ИДЕНТИФИКАТОР", "НАЗВАНИЕ", "СКЛАД", "КОЛ-ВО", "ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ")
 VALUES (001, 'Телевизор', 'Нижегородский', 7, 10000),
        (002, 'Часы напольные', 'Советский', 6, 5000),
        (003, 'Радиоприемник', 'Нижегородский', 10, 7000),
        (004, 'Часы настенные', 'Приокский', 20, 3000),
        (005, 'Холодильник', 'Сормовский', 6, 12000),
        (006, 'Утюг', 'Нижегородский', 30, 2000),
        (007, 'Весы детские', 'Нижегородский', 15, 1500);

INSERT INTO "ПРОКАТ"("НОМЕР", "КЛИЕНТ", "ДАТА", "ПУНКТ ПРОКАТА", "ВЕЩЬ", "СРОК ПРОКАТА", "СУММА, РУБ")
 VALUES (10005, 002, 'Январь', 003, 003, 4, 28000),
        (10006, 003, 'Январь', 003, 007, 1, 1500),
        (10007, 004, 'Январь', 002, 006, 8, 16000),
        (10008, 003, 'Февраль', 002, 005, 4, 48000),
        (10009, 004, 'Февраль', 001, 001, 4, 40000),
        (10010, 005, 'Март', 003, 006, 4, 8000),
        (10011, 005, 'Март', 006, 003, 8, 56000),
        (10012, 001, 'Апрель', 003, 003, 8, 56000),
        (10013, 004, 'Апрель', 004, 002, 2, 10000),
        (10014, 002, 'Май', 005, 007, 2, 3000),
        (10015, 004, 'Май', 006, 004, 1, 3000),
        (10016, 004, 'Май', 002, 001, 11, 110000),
        (10017, 003, 'Июнь', 001, 001, 1, 10000),
        (10018, 005, 'Июль', 001, 007, 1, 1500),
        (10019, 003, 'Август', 003, 002, 4, 20000),
        (10020, 004, 'Август', 005, 002, 4, 20000),
        (10021, 001, 'Август', 003, 001, 2, 20000);
	
	[2021-04-11 21:54:32] 5 rows affected in 28 ms
	[2021-04-11 21:56:50] 6 rows affected in 23 ms
	[2021-04-11 22:05:58] 7 rows affected in 14 ms
	[2021-04-11 22:05:58] 17 rows affected in 12 ms
```


:white_check_mark: **3. Используя оператор SELECT создать запрос для вывода всех строк каждой таблицы. Проверить правильность ввода. При необходимости произвести коррекцию значений операторами INSERT, UPDATE, DELETE.**

```sql
SELECT*
FROM "ЗАКАЗЧИК";
```

| ИДЕНТИФИКАТОР | ФАМИЛИЯ | РАЙОН | СКИДКА, % |
| :--- | :--- | :--- | :--- |
| 1 | Жалнин | Приокский | 2 |
| 2 | Семенов | Советский | 6 |
| 3 | Кожаков | Ленинский | 0 |
| 4 | Шерстнев | Автозаводский | 0 |
| 5 | Козлов | Нижегородский | 4 |


```sql
SELECT*
FROM "ПУНКТ ПРОКАТА";
```

| ИДЕНТИФИКАТОР | НОМЕР | РАСПОЛОЖЕНИЕ | КОМИССИОННЫЕ, % |
| :--- | :--- | :--- | :--- |
| 1 | N23 | Нижегородский | 4 |
| 2 | N16 | Советский | 5 |
| 3 | N8 | Сормовский | 7 |
| 4 | N21 | Приокский | 3 |
| 5 | N12 | Нижегородский | 2 |
| 6 | N6 | Канавинский | 5 |


```sql
SELECT*
FROM "ВЕЩИ";
```

| ИДЕНТИФИКАТОР | НАЗВАНИЕ | СКЛАД | КОЛ-ВО | ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ |
| :--- | :--- | :--- | :--- | :--- |
| 1 | Телевизор | Нижегородский | 7 | 10000 |
| 2 | Часы напольные | Советский | 6 | 5000 |
| 3 | Радиоприемник | Нижегородский | 10 | 7000 |
| 4 | Часы настенные | Приокский | 20 | 3000 |
| 5 | Холодильник | Сормовский | 6 | 12000 |
| 6 | Утюг | Нижегородский | 30 | 2000 |
| 7 | Весы детские | Нижегородский | 15 | 1500 |


```sql
SELECT*
FROM "ПРОКАТ";
```

| НОМЕР | КЛИЕНТ | ДАТА | ПУНКТ ПРОКАТА | ВЕЩЬ | СРОК ПРОКАТА | СУММА, РУБ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 10005 | 2 | Январь | 3 | 3 | 4 | 28000 |
| 10006 | 3 | Январь | 3 | 7 | 1 | 1500 |
| 10007 | 4 | Январь | 2 | 6 | 8 | 16000 |
| 10008 | 3 | Февраль | 2 | 5 | 4 | 48000 |
| 10009 | 4 | Февраль | 1 | 1 | 4 | 40000 |
| 10010 | 5 | Март | 3 | 6 | 4 | 8000 |
| 10011 | 5 | Март | 6 | 3 | 8 | 56000 |
| 10012 | 1 | Апрель | 3 | 3 | 8 | 56000 |
| 10013 | 4 | Апрель | 4 | 2 | 2 | 10000 |
| 10014 | 2 | Май | 5 | 7 | 2 | 3000 |
| 10015 | 4 | Май | 6 | 4 | 1 | 3000 |
| 10016 | 4 | Май | 2 | 1 | 11 | 110000 |
| 10017 | 3 | Июнь | 1 | 1 | 1 | 10000 |
| 10018 | 5 | Июль | 1 | 7 | 1 | 1500 |
| 10019 | 3 | Август | 3 | 2 | 4 | 20000 |
| 10020 | 4 | Август | 5 | 2 | 4 | 20000 |
| 10021 | 1 | Август | 3 | 1 | 2 | 20000 |



:white_check_mark: **4. Создать запросы для вывода:**

• всех различных фамилий заказчиков и размеров их скидок;
```sql
SELECT DISTINCT "ФАМИЛИЯ"
FROM "ЗАКАЗЧИК";
```
| ФАМИЛИЯ |
| :--- |
| Кожаков |
| Козлов |
| Жалнин |
| Шерстнев |
| Семенов |

• всех различных районов проживания заказчиков;
```sql
SELECT DISTINCT "РАЙОН"
FROM "ЗАКАЗЧИК";
```
| РАЙОН |
| :--- |
| Приокский |
| Ленинский |
| Нижегородский |
| Автозаводский |
| Советский |

• всех названий прокатных пунктов и их мест расположения.
```sql
SELECT "НОМЕР", "РАСПОЛОЖЕНИЕ"
FROM "ПУНКТ ПРОКАТА"
```
| НОМЕР | РАСПОЛОЖЕНИЕ |
| :--- | :--- |
| N23 | Нижегородский |
| N16 | Советский |
| N8 | Сормовский |
| N21 | Приокский |
| N12 | Нижегородский |
| N6 | Канавинский |

:white_check_mark: **5. Создав запрос получить следующую информацию:**

• идентификаторы и фамилии заказчиков, проживающих в Приокском или Сормовском районе или тех, чьи фамилии оканчиваются на “ин”;

```sql
SELECT "ИДЕНТИФИКАТОР", "ФАМИЛИЯ"
FROM "ЗАКАЗЧИК"
WHERE "РАЙОН" = 'Сормовский' OR "РАЙОН" = 'Приокский' OR "ФАМИЛИЯ" LIKE '%ин'
```

| ИДЕНТИФИКАТОР | ФАМИЛИЯ |
| :--- | :--- |
| 1 | Жалнин |


• номер, дата, срок проката и сумма для тех записей, где сумма проката более 2000руб. Отсортировать по возрастанию суммы и срока проката;

```sql
SELECT "НОМЕР", "ДАТА", "СРОК ПРОКАТА", "СУММА, РУБ"
FROM "ПРОКАТ"
WHERE "СУММА, РУБ" > 2000
ORDER BY "СУММА, РУБ"
```

| НОМЕР | ДАТА | СРОК ПРОКАТА | СУММА, РУБ |
| :--- | :--- | :--- | :--- |
| 10015 | Май | 1 | 3000 |
| 10014 | Май | 2 | 3000 |
| 10010 | Март | 4 | 8000 |
| 10013 | Апрель | 2 | 10000 |
| 10017 | Июнь | 1 | 10000 |
| 10007 | Январь | 8 | 16000 |
| 10021 | Август | 2 | 20000 |
| 10019 | Август | 4 | 20000 |
| 10020 | Август | 4 | 20000 |
| 10005 | Январь | 4 | 28000 |
| 10009 | Февраль | 4 | 40000 |
| 10008 | Февраль | 4 | 48000 |
| 10012 | Апрель | 8 | 56000 |
| 10011 | Март | 8 | 56000 |
| 10016 | Май | 11 | 110000 |


• названия вещей и адрес складирования, для вещей, оставшихся в количестве не менее 7.

```sql
SELECT "НАЗВАНИЕ", "СКЛАД"
FROM "ВЕЩИ"
WHERE "КОЛ-ВО" >= 7
```

| НАЗВАНИЕ | СКЛАД |
| :--- | :--- |
| Телевизор | Нижегородский |
| Радиоприемник | Нижегородский |
| Часы настенные | Приокский |
| Утюг | Нижегородский |
| Весы детские | Нижегородский |

  
:white_check_mark: **6. На основании данных о прокате вещей вывести все данные в таком формате:**

• фамилия клиента, название пункта проката, дата, номер прокатной квитанции. Отсортировать по первым двум полям;

```sql
SELECT "ЗАКАЗЧИК"."ФАМИЛИЯ", "ПУНКТ ПРОКАТА"."НОМЕР", "ПРОКАТ"."ДАТА", "ПРОКАТ"."НОМЕР"
FROM "ПРОКАТ", "ЗАКАЗЧИК", "ПУНКТ ПРОКАТА"
WHERE "ПРОКАТ"."КЛИЕНТ" = "ЗАКАЗЧИК"."ИДЕНТИФИКАТОР" AND "ПРОКАТ"."ПУНКТ ПРОКАТА" = "ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР"
ORDER BY "ЗАКАЗЧИК"."ФАМИЛИЯ", "ПУНКТ ПРОКАТА"."НОМЕР"  -- только в юникоде цифры не по порядку идут
```
| ФАМИЛИЯ | НОМЕР | ДАТА | НОМЕР |
| :--- | :--- | :--- | :--- |
| Жалнин | N8 | Август | 10021 |
| Жалнин | N8 | Апрель | 10012 |
| Козлов | N23 | Июль | 10018 |
| Козлов | N6 | Март | 10011 |
| Козлов | N8 | Март | 10010 |
| Кожаков | N16 | Февраль | 10008 |
| Кожаков | N23 | Июнь | 10017 |
| Кожаков | N8 | Август | 10019 |
| Кожаков | N8 | Январь | 10006 |
| Семенов | N12 | Май | 10014 |
| Семенов | N8 | Январь | 10005 |
| Шерстнев | N12 | Август | 10020 |
| Шерстнев | N16 | Май | 10016 |
| Шерстнев | N16 | Январь | 10007 |
| Шерстнев | N21 | Апрель | 10013 |
| Шерстнев | N23 | Февраль | 10009 |
| Шерстнев | N6 | Май | 10015 |

	
• название пункта проката, дата, название вещи, сумма.

```sql
SELECT "ПУНКТ ПРОКАТА"."НОМЕР", "ПРОКАТ"."ДАТА", "ВЕЩИ"."НАЗВАНИЕ", "ПРОКАТ"."СУММА, РУБ"
FROM "ПРОКАТ", "ПУНКТ ПРОКАТА", "ВЕЩИ"
WHERE "ПРОКАТ"."ПУНКТ ПРОКАТА" = "ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР" AND "ПРОКАТ"."ВЕЩЬ" = "ВЕЩИ"."ИДЕНТИФИКАТОР"
```

| НОМЕР | ДАТА | НАЗВАНИЕ | СУММА, РУБ |
| :--- | :--- | :--- | :--- |
| N8 | Январь | Радиоприемник | 28000 |
| N8 | Январь | Весы детские | 1500 |
| N16 | Январь | Утюг | 16000 |
| N16 | Февраль | Холодильник | 48000 |
| N23 | Февраль | Телевизор | 40000 |
| N8 | Март | Утюг | 8000 |
| N6 | Март | Радиоприемник | 56000 |
| N8 | Апрель | Радиоприемник | 56000 |
| N21 | Апрель | Часы напольные | 10000 |
| N12 | Май | Весы детские | 3000 |
| N6 | Май | Часы настенные | 3000 |
| N16 | Май | Телевизор | 110000 |
| N23 | Июнь | Телевизор | 10000 |
| N23 | Июль | Весы детские | 1500 |
| N8 | Август | Часы напольные | 20000 |
| N12 | Август | Часы напольные | 20000 |
| N8 | Август | Телевизор | 20000 |


7. Вывести:

• названия прокатных пунктов, которые отдавали в прокат утюги или оказывали услуги клиентам своего района;
```sql
SELECT DISTINCT "ПУНКТ ПРОКАТА"."НОМЕР"
FROM "ПРОКАТ", "ПУНКТ ПРОКАТА", "ЗАКАЗЧИК"
WHERE  ("ПРОКАТ"."КЛИЕНТ" = "ЗАКАЗЧИК"."ИДЕНТИФИКАТОР" AND
	"ЗАКАЗЧИК"."РАЙОН" = "ПУНКТ ПРОКАТА"."РАСПОЛОЖЕНИЕ" AND
        "ПРОКАТ"."ПУНКТ ПРОКАТА" = "ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР") OR
       ("ПРОКАТ"."ВЕЩЬ" = 006 AND "ПРОКАТ"."ПУНКТ ПРОКАТА" = "ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР")
```

| НОМЕР |
| :--- |
| N23 |
| N16 |
| N8 |


•имена и адреса заказчиков, бравших в прокат вещи со стоимостью проката более 8000руб не ранее февраля месяца. Вывести вместе с названиями прокатных пунктов, где были взяты вещи, проиведя по ним сортировку;

```sql
SELECT DISTINCT "ЗАКАЗЧИК"."ФАМИЛИЯ", "ЗАКАЗЧИК"."РАЙОН", "ПУНКТ ПРОКАТА"."НОМЕР"
FROM "ЗАКАЗЧИК", "ПРОКАТ", "ВЕЩИ", "ПУНКТ ПРОКАТА"
WHERE "ПРОКАТ"."ДАТА" <> 'Январь' AND "ВЕЩИ"."ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ" > 8000 AND
      "ПРОКАТ"."КЛИЕНТ" = "ЗАКАЗЧИК"."ИДЕНТИФИКАТОР" AND "ПРОКАТ"."ВЕЩЬ" = "ВЕЩИ"."ИДЕНТИФИКАТОР" AND
      "ПРОКАТ"."ПУНКТ ПРОКАТА" = "ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР"
```

| ФАМИЛИЯ | РАЙОН | НОМЕР |
| :--- | :--- | :--- |
| Кожаков | Ленинский | N16 |
| Кожаков | Ленинский | N23 |
| Шерстнев | Автозаводский | N23 |
| Жалнин | Приокский | N8 |
| Шерстнев | Автозаводский | N16 |


• название и прокатную цену вещей взятых заказчиком Кожаковым в прокатных пунктах других районов;



• название и оставшееся количество вещей, которые отдавали более чем в одном прокатном пункте.


8. Создать запрос для модификации всех значений столбца с суммарной величиной оплаты таблицы прокат, чтобы он содержал истинную сумму, оплачиваемую клиентом ( с учетом скидки). Вывести новые значения.


9. Расширить таблицу с данными о прокате столбцом, содержащим величину взимаемых комиссионых. Создать запрос для ввода конкретных значений во все строки таблицы проката.


# Уровень 2

1. Используя операцию IN (NOT IN)  реализовать следующие запросы:

• найти вещи, бравшиеся в прокат заказчиками с размером скидки более 2%;

```sql
SELECT DISTINCT "ВЕЩИ"."НАЗВАНИЕ"
from "ЗАКАЗЧИК", "ПРОКАТ", "ВЕЩИ"
WHERE "ПРОКАТ"."КЛИЕНТ" IN (SELECT "ЗАКАЗЧИК"."ИДЕНТИФИКАТОР" WHERE "ЗАКАЗЧИК"."СКИДКА, %" NOT IN(0, 1, 2))
AND "ПРОКАТ"."ВЕЩЬ" = "ВЕЩИ"."ИДЕНТИФИКАТОР"
```

| НАЗВАНИЕ |
| :--- |
| Весы детские |
| Утюг |
| Радиоприемник |


• найти все вещи, бравшиеся в прокат заказчиком, бравшим что-либо в прокатных пунктах своего района;

```sql
SELECT "ВЕЩИ"."НАЗВАНИЕ", "ЗАКАЗЧИК"."ФАМИЛИЯ"
from "ЗАКАЗЧИК", "ПРОКАТ", "ВЕЩИ", "ПУНКТ ПРОКАТА"
WHERE "ВЕЩИ"."ИДЕНТИФИКАТОР" IN (
    SELECT "ПРОКАТ"."ВЕЩЬ" WHERE "ЗАКАЗЧИК"."РАЙОН" IN (
        SELECT "ПУНКТ ПРОКАТА"."РАСПОЛОЖЕНИЕ"
        WHERE "ПРОКАТ"."ПУНКТ ПРОКАТА" = "ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР"
        AND "ПРОКАТ"."КЛИЕНТ" = "ЗАКАЗЧИК"."ИДЕНТИФИКАТОР"
    ))
```

| НАЗВАНИЕ | ФАМИЛИЯ |
| :--- | :--- |
| Весы детские | Козлов |


• запросы заданий 7.b, 7.с.

```sql

```
  
 
2. Используя операции ALL-ANY реализовать следующие запросы:

• определить те вещи, которые брались летом на самый продолжительный срок;

```sql
SELECT lab1schema."ВЕЩИ"."НАЗВАНИЕ", lab1schema."ПРОКАТ"."СРОК ПРОКАТА"
FROM lab1schema."ПРОКАТ", lab1schema."ВЕЩИ"
WHERE "ПРОКАТ"."ВЕЩЬ" = "ВЕЩИ"."ИДЕНТИФИКАТОР"
AND "СРОК ПРОКАТА" >= ALL (SELECT "СРОК ПРОКАТА" FROM lab1schema."ПРОКАТ" WHERE "ПРОКАТ"."ДАТА" IN ('Август', 'Июнь', 'Июль'))
AND "ПРОКАТ"."ДАТА" IN ('Август', 'Июнь', 'Июль')
```

| НАЗВАНИЕ | СРОК ПРОКАТА |
| :--- | :--- |
| Часы напольные | 4 |
| Часы напольные | 4 |


• найти прокатные пункты, отдававшие вещи с самой большой ценой;

```sql
SELECT lab1schema."ВЕЩИ"."ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ", lab1schema."ПУНКТ ПРОКАТА"."НОМЕР"
FROM lab1schema."ПРОКАТ", lab1schema."ПУНКТ ПРОКАТА", lab1schema."ВЕЩИ"
WHERE "ПРОКАТ"."ПУНКТ ПРОКАТА" = lab1schema."ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР"
AND "ПРОКАТ"."ВЕЩЬ" = "ВЕЩИ"."ИДЕНТИФИКАТОР"
AND "ВЕЩИ"."ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ" >= ALL (
    SELECT "ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ"
    FROM lab1schema."ВЕЩИ"
    )
```

| ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ | НОМЕР |
| :--- | :--- |
| 12000 | N16 |


• найти таких заказчиков, которые имеют такой же размер скидки, как кто-либо из бравших на прокат радиоприемник;

```sql
SELECT DISTINCT lab1schema."ЗАКАЗЧИК"."ФАМИЛИЯ"
FROM lab1schema."ПРОКАТ", lab1schema."ВЕЩИ", lab1schema."ЗАКАЗЧИК"
WHERE "СКИДКА, %" = ANY(
    SELECT "СКИДКА, %"
    WHERE "ПРОКАТ"."КЛИЕНТ" = "ЗАКАЗЧИК"."ИДЕНТИФИКАТОР"
    AND "ПРОКАТ"."ВЕЩЬ" = 3
    )
```

| ФАМИЛИЯ |
| :--- |
| Козлов |
| Жалнин |
| Семенов |


• запрос задания 7.а.

```sql

```

  
3. Используя операцию UNION получить адреса проживания заказчиков и места расположения прокатных пунктов.

```sql
SELECT "РАЙОН" FROM lab1schema."ЗАКАЗЧИК"
UNION
SELECT "РАСПОЛОЖЕНИЕ" FROM lab1schema."ПУНКТ ПРОКАТА"
```

| РАЙОН |
| :--- |
| Сормовский |
| Приокский |
| Ленинский |
| Канавинский |
| Нижегородский |
| Автозаводский |
| Советский |


4. Используя операцию EXISTS ( NOT EXISTS ) реализовать нижеследующие запросы. В случае, если для текущего состояния БД запрос будет выдавать пустое множество строк, требуется указать какие добавления в БД необходимо провести.

• найти две самые дорогие вещи, сдававшиеся в прокат не позднее октября;

```sql
SELECT "НАЗВАНИЕ" FROM lab1schema."ВЕЩИ", lab1schema."ПРОКАТ"
WHERE EXISTS(
    SELECT "НОМЕР"
    WHERE "ВЕЩЬ" = "ИДЕНТИФИКАТОР"
    AND "ДАТА" NOT IN('Ноябрь', 'Декабрь')
    )
GROUP BY "НАЗВАНИЕ"
ORDER BY MAX("ПРОКАТНАЯ ЦЕНА ЗА НЕДЕЛЮ, РУБ") DESC LIMIT 2
```

| НАЗВАНИЕ |
| :--- |
| Холодильник |
| Телевизор |


• найти прокатные пункты, сдававшие все вещи всем заказчикам из Нижегородского района;

```sql

```

• найти заказчиков не бравших в прокат вещи ценой мене 5000руб. в прокатных пунктах чужих районов;

```sql

```

• найти заказчиков, бравших вещи во всех прокатных пунктах с размером комиссионных менее 5%.

```sql

```
  
  
5. Реализовать запросы с использованием аггрегатных функций:

• найти средний срок проката вещей, бравшихся в прокатных пунктах Советского района;

```sql
SELECT AVG("СРОК ПРОКАТА")
FROM lab1schema."ПРОКАТ", lab1schema."ПУНКТ ПРОКАТА"
WHERE "ПРОКАТ"."ПУНКТ ПРОКАТА" = "ИДЕНТИФИКАТОР"
AND "РАСПОЛОЖЕНИЕ" = 'Сормовский'
```

| avg |
| :--- |
| 3.8333333333333333 |


• найти заказчика, имеющего минимальную скидку среди бравших вещи в бюро проката N8;

```sql
SELECT MIN("СКИДКА, %") AS SmallestSale, "ФАМИЛИЯ"
FROM lab1schema."ПРОКАТ", lab1schema."ПУНКТ ПРОКАТА", lab1schema."ЗАКАЗЧИК"
WHERE "ПРОКАТ"."ПУНКТ ПРОКАТА" = lab1schema."ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР"
AND lab1schema."ПУНКТ ПРОКАТА"."НОМЕР" = 'N8'
GROUP BY lab1schema."ЗАКАЗЧИК"."ФАМИЛИЯ" LIMIT 1
```

| smallestsale | ФАМИЛИЯ |
| :--- | :--- |
| 0 | Кожаков |


• найти те записи о прокате, где стоимость проката больше средней по району, в котором располагается бюро найма;

```sql
SELECT "РАСПОЛОЖЕНИЕ",AVG("ПРОКАТ"."СУММА, РУБ") as AvgSum
FROM lab1schema."ПРОКАТ", lab1schema."ПУНКТ ПРОКАТА"
WHERE "ПРОКАТ"."ПУНКТ ПРОКАТА" = lab1schema."ПУНКТ ПРОКАТА"."ИДЕНТИФИКАТОР"
GROUP BY "РАСПОЛОЖЕНИЕ"
HAVING AVG("ПРОКАТ"."СУММА, РУБ") < "ПРОКАТ"."СУММА, РУБ"
```

• найти общее число вещей, бравшихся Семеновым.

```sql
SELECT "ЗАКАЗЧИК"."ФАМИЛИЯ" , count("КЛИЕНТ")
FROM lab1schema."ПРОКАТ", lab1schema."ЗАКАЗЧИК"
WHERE "КЛИЕНТ" = "ЗАКАЗЧИК"."ИДЕНТИФИКАТОР"
AND "ЗАКАЗЧИК"."ФАМИЛИЯ" = 'Семенов'
GROUP BY "ЗАКАЗЧИК"."ФАМИЛИЯ"
```

| ФАМИЛИЯ | count |
| :--- | :--- |
| Семенов | 2 |


6. Используя средства группировки реализовать следующие запросы:

• найти суммарную величину стоимости проката для каждой вещи;

```sql

```

• определить для каждой вещи средний срок проката за осенний период;

```sql

```

• найти для каждого заказчика, бравшего вещи во всех бюро проката Советского района, число различных бравшихся в прокат вещей;

```sql

```

• получить сводную таблицу “бюро проката - вещь-суммарная стоимость проката”.

```sql

```


