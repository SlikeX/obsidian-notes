1) null и undefined при нестрогом равенстве равны друг гругу и ничему другому
alert( null == undefined ); // true
поэтому работает след фишка
```javascript
alert( null > 0 );  // (1) false
alert( null == 0 ); // (2) false
alert( null >= 0 ); // (3) true
```

С точки зрения математики это странно. Результат последнего сравнения говорит о том, что "`null` больше или равно нулю", тогда результат одного из сравнений выше должен быть `true`, но они оба ложны.

Причина в том, что нестрогое равенство и сравнения `> < >= <=` работают по-разному. Сравнения преобразуют `null` в число, рассматривая его как `0`. Поэтому выражение (3) `null >= 0` истинно, а `null > 0` ложно.

С другой стороны, для нестрогого равенства `==` значений `undefined` и `null` действует особое правило: эти значения ни к чему не приводятся, они равны друг другу и не равны ничему другому. Поэтому (2) `null == 0` ложно.

2) || возвращает первый истинный или последний
 alert( 1 || 0 ); // 1 alert( true || 'no matter what' ); // true alert( null || 1 ); // 1 (первое истинное значение) alert( null || 0 || 1 ); // 1 (первое истинное значение) alert( undefined || null || 0 ); // 0 (поскольку все ложно, возвращается последнее значение)

3) && возвращает первый ложный или последний
 Можно передать несколько значений подряд. В таком случае возвратится первое «ложное» значение, на котором остановились вычисления.
`alert( 1 && 2 && null && 3 ); // null`

Когда все значения верны, возвращается последнее

`alert( 1 && 2 && 3 ); // 3`

4) Никогда не добавляйте перевод строки между `return` и его значением

Для длинного выражения в `return` может быть заманчиво разместить его на нескольких отдельных строках, например так:

`return  (some + long + expression + or + whatever * f(a) + f(b))`

Код не выполнится, потому что интерпретатор JavaScript подставит точку с запятой после `return`. Для него это будет выглядеть так:

`return_;_  (some + long + expression + or + whatever * f(a) + f(b))`

Таким образом, это фактически стало пустым `return`.

Если мы хотим, чтобы возвращаемое выражение занимало несколько строк, нужно начать его на той же строке, что и `return`. Или, хотя бы, поставить там открывающую скобку, вот так:

`return (   some + long + expression   + or +   whatever * f(a) + f(b)   )`

И тогда всё сработает, как задумано.

5) **В строгом режиме, когда Function Declaration находится в блоке `{...}`, функция доступна везде внутри блока. Но не снаружи него.**

Для примера давайте представим, что нам нужно объявить функцию `welcome()` в зависимости от значения переменной `age`, которое мы получим во время выполнения кода. И затем запланируем использовать её когда-нибудь в будущем.

Если мы попробуем использовать Function Declaration, это не заработает так, как задумывалось:

![[Pasted image 20221213102206.png]]

Это произошло, так как объявление Function Declaration видимо только внутри блока кода, в котором располагается.

Вот ещё один пример:


![[Pasted image 20221213102227.png]]

Что можно сделать, чтобы `welcome` была видима снаружи `if`?

Верным подходом будет воспользоваться функцией, объявленной при помощи Function Expression, и присвоить значение `welcome` переменной, объявленной снаружи `if`, что обеспечит нам нужную видимость.

Такой код заработает, как ожидалось:


![[Pasted image 20221213102244.png]]

Или мы могли бы упростить это ещё сильнее, используя условный оператор `?`:

![[Pasted image 20221213102259.png]]

6) Мы даже можем вызвать функцию вообще без объекта:

`function sayHi() {   alert(this); }  sayHi(); // undefined`

В строгом режиме (`"use strict"`) в таком коде значением `this` будет являться `undefined`. Если мы попытаемся получить доступ к `this.name` – это вызовет ошибку.

В нестрогом режиме значением `this` в таком случае будет _глобальный объект_ (`window` в браузерe, мы вернёмся к этому позже в главе [Глобальный объект](https://learn.javascript.ru/global-object)). Это – исторически сложившееся поведение `this`, которое исправляется использованием строгого режима (`"use strict"`).

Обычно подобный вызов является ошибкой программирования. Если внутри функции используется `this`, тогда она ожидает, что будет вызвана в контексте какого-либо объекта.

7) Каким будет результат при обращении к свойству объекта `ref`? Почему?

`function makeUser() {   
return {     
name: "John",     
ref: this   }; 
}  
let user = makeUser();  
alert( user.ref.name ); // Каким будет результат?`

решение

**Ответ: ошибка.**


`function makeUser() {   
return {     
name: "John",     
ref: this   };
}  
let user = makeUser();
alert( user.ref.name ); // Error: Cannot read property 'name' of undefined`

Это потому, что правила, которые определяют значение `this`, никак не смотрят на объявление объекта. Важен лишь момент вызова.

Здесь значение `this` внутри `makeUser()` равно `undefined`, потому что оно вызывается как функция, а не через «точечный» синтаксис как метод.

Значение `this` одно для всей функции, блоки кода и объектные литералы на него не влияют.

Таким образом, `ref: this` фактически принимает текущее `this` функции `makeUser()`.

Мы можем переписать функцию и вернуть то же самое `this` со значением `undefined`:

`function makeUser(){   
return this; // на этот раз нет литерала объекта }  
alert( makeUser().name ); // Error: Cannot read property 'name' of undefined`

Как вы можете видеть, результат `alert( makeUser().name )` совпадает с результатом `alert( user.ref.name )` из предыдущего примера.

Вот противоположный случай:

`function makeUser() {   
return {     
name: "John",    
_ref() {       
return this;     
}_ 
}; }  
let user = makeUser();  
alert( user.ref().name ); // John`

Теперь это работает, поскольку `user.ref()` – это метод. И значением `this` становится объект перед точкой `.`.

8) Свойства, чьи ключи – символы, не перебираются циклом `for..in`.

Например:


`let id = Symbol("id"); 
let user = {   name: "Вася",   age: 30,   [id]: 123 }; 
_for (let key in user) alert(key); // name, age (свойства с ключом-символом нет среди перечисленных)_  
// хотя прямой доступ по символу работает alert( "Напрямую: " + user[id] );`

Это – часть общего принципа «сокрытия символьных свойств». Если другая библиотека или скрипт будут работать с нашим объектом, то при переборе они не получат ненароком наше символьное свойство. `Object.keys(user)` также игнорирует символы.

А вот [Object.assign](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/assign), в отличие от цикла `for..in`, копирует и строковые, и символьные свойства:

`let id = Symbol("id"); 
let user = {   [id]: 123 };  
let clone = Object.assign({}, user); 
alert( clone[id] ); // 123`

Здесь нет никакого парадокса или противоречия. Так и задумано. Идея заключается в том, что, когда мы клонируем или объединяем объекты, мы обычно хотим скопировать _все_ свойства (включая такие свойства с ключами-символами, как, например, `id` в примере выше)

9) Глобальные символы

Итак, как мы видели, обычно все символы уникальны, даже если их имена совпадают. Но иногда мы наоборот хотим, чтобы символы с одинаковыми именами были одной сущностью. Например, разные части нашего приложения хотят получить доступ к символу `"id"`, подразумевая именно одно и то же свойство.

Для этого существует _глобальный реестр символов_. Мы можем создавать в нём символы и обращаться к ним позже, и при каждом обращении нам гарантированно будет возвращаться один и тот же символ.

Для чтения (или, при отсутствии, создания) символа из реестра используется вызов `Symbol.for(key)`.

Он проверяет глобальный реестр и, при наличии в нём символа с именем `key`, возвращает его, иначе же создаётся новый символ `Symbol(key)` и записывается в реестр под ключом `key`.

Например:


`// читаем символ из глобального реестра и записываем его в переменную 
let id = Symbol.for("id"); // если символа не существует, он будет создан  
// читаем его снова и записываем в другую переменную (возможно, из другого места кода) 
let idAgain = Symbol.for("id");  // проверяем -- это один и тот же символ alert( id === idAgain ); // true`

Символы, содержащиеся в реестре, называются _глобальными символами_. Если вам нужен символ, доступный везде в коде – используйте глобальные символы.


10) Перечитать про дескрипторы пару раз https://learn.javascript.ru/property-descriptors
11) И геттеры и сеттеры https://learn.javascript.ru/property-accessors

12) null == undefined
13) for...of использует Symbol.iterator для перебора под капотом
14)  _Итерируемые объекты_ – это объекты, которые реализуют метод `Symbol.iterator`, как было описано выше.
-     Псевдомассивы_ – это объекты, у которых есть индексы и свойство `length`, то есть, они выглядят как массивы.

15) Написать деструктуризацию для объекта и массива

16) [Object.seal(obj)](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/seal)

Запрещает добавлять/удалять свойства. Устанавливает `configurable: false` для всех существующих свойств.

[Object.freeze(obj)](https://developer.mozilla.org/ru/docs/Web/JavaScript/Reference/Global_Objects/Object/freeze)

Запрещает добавлять/удалять/изменять свойства. Устанавливает `configurable: false, writable: false` для всех существующих свойств.