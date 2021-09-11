# super

Ключевое слово **super** используется для вызова функций, принадлежащих родителю объекта.

Выражения `super.prop` и `super[expr]` действительны в любом определении метода в классах и в литералах объекта.

## Синтаксис

> super([arguments]); // вызов родительского конструктора.
> super.functionOnParent([arguments]);

## Описание

В конструкторе ключевое слово `super()` используется как функция, вызывающая родительский конструктор. Её необходимо вызвать до первого обращения к ключевому слову `this` в теле конструктора. Ключевое слово `super` также может быть использовано для вызова функций родительского объекта.

## Пример
### Использование super в классах

В этом примере `super()` вызывается, чтобы не повторять части конструктора, одинаковые для классов `Rectangle` и `Square`.

     class Rectangle {
       constructor(height, width) {
         this.name = 'Rectangle';
         this.height = height;
         this.width = width;
       }
       sayName() {
         console.log('Hi, I am a ', this.name + '.');
       }
       get area() {
         return this.height * this.width;
       }
       set area(value) {
         this._area = value;
       }
     }
     
    class Square extends Rectangle {
       constructor(length) {
         this.height; // ReferenceError, super должен быть вызван первым!
     
         // Здесь вызывается конструктор родительского класса с длинами,
         // указанными для ширины и высоты класса Rectangle
         super(length, length);
     
         // Примечание: в производных классах super() необходимо вызывать, прежде чем
         // использовать 'this'. Если этого не сделать, произойдет ошибка ReferenceError.
         this.name = 'Square';
       }
     }

### Вызов статических методов через super

Вы также можете вызывать `super` для статических методов.

     class Rectangle {
       static logNbSides() {
         return 'У меня 4 стороны';
       }
     }
     
     class Square extends Rectangle {
       static logDescription() {
         return super.logNbSides() + ', равные между собой';
       }
     }
     Square.logDescription(); // 'У меня 4 стороны, равные между собой'

### Удаление свойств через super вызывает ошибку

Вы не можете использовать оператор delete и `super.prop` или `super[expr]` для удаления свойств родительского класса, он выдаст: ReferenceError.

     class Base {
       constructor() {}
       foo() {}
     }
     class Derived extends Base {
       constructor() {}
       delete() {
         delete super.foo; // это плохо
       }
     }
     
     new Derived().delete(); // ReferenceError: invalid delete involving 'super'. 

### super.prop не может переопределять свойства, защищённые от записи

При определении незаписываемых свойств с помощью, например, Object.defineProperty, super не может перезаписать значение свойства.

     class X {
       constructor() {
         Object.defineProperty(this, 'prop', {
           configurable: true,
           writable: false,
           value: 1
         });
       }
     }
     
     class Y extends X {
       constructor() {
         super();
       }
       foo() {
         super.prop = 2;   // Невозможно перезаписать значение.
       }
     }
     
     var y = new Y();
     y.foo(); // TypeError: "prop" доступен только для чтения
     console.log(y.prop); // 1

### Использование super.prop в объектных литералах     

Super также можно использовать в объекте инициализатора / литерала. В этом примере метод определяют два объекта. Во втором объекте super вызывает метод первого объекта. Это работает благодаря `Object.setPrototypeOf()`, с помощью которого мы можем установить прототип для `obj2` в `obj1`, так что `super` может найти `method1` в `obj1`.

     var obj1 = {
       method1() {
         console.log('method 1');
       }
     }
     
     var obj2 = {
       method2() {
         super.method1();
       }
     }
     
     Object.setPrototypeOf(obj2, obj1);
     obj2.method2(); // выведет "method 1"

    Спецификации и поддержку браузерами см. [здесь].(https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Operators/super)