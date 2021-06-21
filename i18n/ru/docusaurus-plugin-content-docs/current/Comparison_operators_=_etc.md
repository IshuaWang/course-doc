---
title: 'Операторы сравнения (=, >, <, ...)'
---

*Операторы сравнения* создают [свойства](Properties.md), возвращаемым значением которых является результат операции сравнения. Значения созданных свойств принадлежат [встроенному классу](Built-in_classes.md) `BOOLEAN`.

В платформе на данный момент поддерживаются следующие операторы сравнения:

|Оператор    |Название           |Описание                                                                                        |Пример  |Результат|
|------------|-------------------|------------------------------------------------------------------------------------------------|--------|---------|
|`=` или `==`|Равенство          |Принимает два операнда на вход, возвращает `TRUE`, если операнды равны                          |`5 = 5` или `5 == 5`|`TRUE`|
|`!=`        |Неравенство        |Принимает два операнда на вход, возвращает `TRUE`, если операнды не равны                       |`3 != 5`|`TRUE`   |
|`>`, `<`    |Строгое сравнение  |Принимают два операнда на вход, возвращают `TRUE`, если условие строгого сравнения выполняется  |`3 > 5` |`NULL`   |
|`>=`, `<=`  |Нестрогое сравнение|Принимают два операнда на вход, возвращают `TRUE`, если условие нестрогого сравнения выполняется|`4 <= 5`|`TRUE`   |

Во всех операторах, если один из операндов `NULL`, результат также будет равняться `NULL`.

### Язык

Описание [операторов сравнения](Comparison_operators.md).

### Примеры


```lsf
equalBarcodes = barcode(a) == barcode(b);
outOfIntervalValue1(value, left, right) = value < left OR value > right;
outOfIntervalValue2(value, left, right) = NOT (value >= left AND value <= right);
```