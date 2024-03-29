# Типы данных в Java Script

Язык программирования Java Script является "динамически типизированным", то есть переменная может содержать любые данные: сейчас она содержит число, а через секунду мы задаем строку:

```jsx
let number = 1;
number = "one";
```

Это значит, что сама переменная не привязана к определенному типу, тип данных присваивается переменной вместе со значением.

Существуют следующие типы данных:

- число
- строка
- булевый тип (логический)
- специальные значения: null и undefined
- и некоторые другие

Узнать текущий тип данных можно с помощью оператора `typeof`:

![screenshot](/pictures/typeof.png)

# Тип данных number (число)
 Числовой тип данных (number) представляет как целочисленные значения, так и числа с плавающей точкой.

 Существует множество операций для чисел, например, умножение *, деление /, сложение +, вычитание - и так далее.

Кроме обычных чисел, существуют так называемые «специальные числовые значения», которые относятся к этому типу данных: Infinity, -Infinity и NaN.

Infinity представляет собой математическую бесконечность ∞. Это особое значение, которое больше любого числа.

Мы можем получить его в результате деления на ноль:

```jsx 
alert( 1 / 0 ); // Infinity 
```

Или задать его явно:

```jsx  
alert( Infinity ); // Infinity
```
NaN означает вычислительную ошибку. Это результат неправильной или неопределённой математической операции, например:

```jsx 
alert( "не число" / 2 ); // NaN, такое деление является ошибкой
```
Значение NaN «прилипчиво». Любая операция с NaN возвращает NaN:

```jsx  
alert( "не число" / 2 + 5 ); // NaN
```
Если где-то в математическом выражении есть NaN, то результатом вычислений с его участием будет NaN.

