---
title: 'Группировка (GROUP)'
---

Оператор *группировки* создает [свойство](Properties.md), которое разбивает все наборы объектов в системе на группы, и с учетом заданного порядка вычисляет для каждой такой группы [агрегирующую функцию](Set_operations.md#func). Соответственно, множество, на котором вычисляется эта агрегирующая функция, определяется как все наборы объектов, принадлежащие данной группе. 

Группы в этом операторе задаются как множество свойств (*группировок*), порядок задается как список свойств и признак возрастания или убывания. Если агрегирующая функция не [коммутативна](Set_operations.md#commutative-broken), то порядок должен быть однозначно определяемым. 


:::info
Однозначно определяемого порядка можно гарантированно добиться, если при задании порядка, например, указать идентификаторы всех объектов, для которых выполняется группировка
:::

Кроме стандартных видов агрегирующих функций для группировки есть три дополнительных вида: `EQUAL`, `AGGR` и `NAGGR`.

-   `EQUAL` является частным случаем агрегирующей функции `MAX` (или `MIN`), добавляя [ограничение](Constraints.md) на одинаковость значения операнда агрегирующей функции внутри каждой группы. 
-   `AGGR` и `NAGGR` являются частным случаем `EQUAL`, но с еще более строгим ограничением: для каждой группы существует не более одного набора объектов, операнд агрегирующей функции является одним из объектов, а группировки включают в себя все остальные объекты. Агрегирующая функция `NAGGR` отличается от `AGGR` только тем, что в случае ее использования не создается ограничение (предполагается, что это ограничение следует из семантики самих свойств операндов и/или группировок).

### Язык

Для объявления свойства, реализующего группировку, используется [оператор `GROUP`](GROUP_operator.md).

### Примеры

```lsf
CLASS Game;
CLASS Team;
hostGoals = DATA INTEGER (Game);
hostTeam = DATA Team (Game);
hostGoalsScored(team) = GROUP SUM hostGoals(Game game) BY hostTeam(game);

name = DATA STRING[100] (Country);
countryName = GROUP AGGR Country country WHERE country IS Country BY name(country); // получается свойство (STRING[100]) -> Country

CLASS Book;
CLASS Tag;
name = DATA STRING[100] (Tag);
in = DATA BOOLEAN (Book, Tag);

tags(Book b) = GROUP CONCAT name(Tag t) IF in(b, t), ', ' ORDER name(t), t;
```