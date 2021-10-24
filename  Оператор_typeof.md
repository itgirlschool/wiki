# Оператор typeof

Оператор **typeof** позволяет определить тип параметра (число, строка, объект). 

Оператор возвращает строку, содержащую тип ('number', 'string', 'object').

Для *null* оператор возвращает 'object' (это признанная ошибка языка). Для функций оператор возвращает 'function'. Это сделано для удобства, так как типа 'function' не существует.

## Синтаксис

У оператора typeof есть 2 синтаксиса (оба синтаксиса работают одинаково):

`typeof параметр`

`typeof(параметр);`

## Пример  1

Посмотрим, как typeof работает с различными параметрами:

`typeof 1 // 'number'`

`typeof 'str' // 'string'`

`typeof true // 'boolean'`

`typeof undefined // 'undefined'`

`typeof {} // 'object'`

`typeof null // 'object'`

`typeof function() {} // 'function'`

## Пример 2 

Напишем функцию, которая будет выводить только числа:

`function printNumber(number) {`

`if (typeof number === 'number') {`

`	console.log(number);`

`}`

`}`

`printNumber(2);`

`printNumber('str');`

`printNumber(3);`


