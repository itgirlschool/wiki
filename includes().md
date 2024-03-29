  # JavaScript: includes vs indexOf

Начиная с ECMAScript 2016 в JavaScript появился новый метод includes для работы с массивами. По своей сути он очень сильно напоминает indexOf. В этой статье я хочу рассмотреть подробнее для чего был введен этод метод и в чем его отличие от indexOf.

### Массивы

Итак, метод **Array.prototype.includes** определяет содержится ли в массиве искомое значение и возвращает *true* или *false*. Таким образом, в отличие от indexOf, который возвращает целое число, includes возвращает значение типа boolean. Это нововведение поможет разработчикам писать более чистый и понятный код.

Например, вот стандартный пример проверки того, содержится ли элемент в массиве, с помощью indexOf:

`var numbers = [3, 5, 8, 11, 23, 7];`

`if (numbers.indexOf(1) !== -1) {`

`// ...`

`}`

Используя includes, то же самое можно написать так:

`var numbers = [3, 5, 8, 11, 23, 7];`

`if (numbers.includes(1)) {`

`// ...`

`}`

Также при внедрении этого метода были учтены некоторые неочевидные особенности, замеченные при работе с indexOf. В отношении значений NaN поведение этого метода отличается.

Рассмотрим на примере:

`var numbers = [3, 5, 8, 11, 23, 7, NaN];`

`if (numbers.indexOf(NaN) !== -1) {`

` // Этот код не выполнится`

`}`

`if (numbers.includes(NaN)) {`

`// Этот код выполнится`

`}`

Таким образом, indexOf(NaN) всегда возвращает -1, независимо от того содержится ли это значение в массиве, а includes(NaN) возвращает true или false в зависимости от того есть этот элемен в массиве или нет.

## Строки

Аналогичный метод был добавлен и для работы со строками начиная с ECMAScript 2015. Ранее в Firefox в версиях с 18 по 39 этот метод существовал под именем contains, однако из-за проблем совместимости он был переименован в includes().