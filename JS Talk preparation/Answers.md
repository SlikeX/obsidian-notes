**JavaScript Related Questions**

1.    Hosting, be able to create an example of it in code

_Поднятие_ или _hoisting_ — это механизм в JavaScript, в котором переменные и объявления функций, передвигаются вверх своей области видимости перед тем, как код будет выполнен.

## Undefined vs ReferenceError

Перед тем, как мы начнем серьёзно углубляться в этот вопрос, давайте проясним несколько вещей.

 console.log(typeof variable); **// Выводит: undefined**

Это приведет нас к первому заключению. В JavaScript, необъявленной переменной при выполнении кода назначается значение `undefined` , а так же и тип `undefined`.

Вторым заключением будет:

console.log(variable); // **Выводит: ReferenceError: variable is not defined**

В JavaScript, `ReferenceError` появляется при попытке доступа к предварительно необъявленной переменной.

Поведение JavaScript при работе с переменными становится довольно утонченным делом из-за «поднятия». Мы увидим это более детально в следующих параграфах.

Объявление переменных происходит перед выполнением кода.

function hoist() {  
  a = 20;  
  var b = 100;  
}  
  
hoist();  
  
console.log(a);**/*****Доступ как к глобальной переменной вне функции hoist()****Выводит: 20*****/**console.log(b);**/*****Как только b была назначена, она заключена в рамки области видимости функции hoist(). Что означает то, что мы не можем вывести её за рамки функции.****Вывод: ReferenceError: b is not defined*****/**

переменная а записывается в объект window и имеет глобальную область видимости


2.    Closures, be able to create an example of it in code

3.    Have solid understand why we use closures, how it is connected with encapsulation and IIFE

4.    This keyword – basic idea, and its use in common and arrow function with examples

5.    New keyword. How it works

6.    == comparison algorithm

7.    Priority of operations with example

8.    Have solid understanding of types auto conversion, what is unary, binary, ternary operations.

9.    Type of vs instance of show difference in examples.

10. Prototype inheritance, props and cons, be able to realize

11. Primitive vs reference types with example. Pass by value vs pass by reference

12. What is Promise, why should we use it. Promise vs async await, show similarity in examples

13. Fetch api

14. Basic DOM api: update, create, remove classes, attributes. Navigate through DOM tree. Be able to write recursive function to go throught DOM tree.

15. How to add events. Capturing / Bubbling. Event delegation pattern. PreventDefault. Stop propagation. Stop propagation immediate.

16. Differences between click, mousedown, mouseup, mouseover / mouseenter.

17. BOM – navigation , history, location, LocalStorage, SessionStorage

18. Even Loop with examples

19. For In vs For Of. What Is Symbol.Iterator. Create custom interator

20. Interators vs Generators – at least basic knowledge

21. Object descriptors. How for in loop works

22. Rest operator (…) destruturing object properties

23. Js Errors. Throw, catch, create custom errors.

Optional:

1.    Immutable types, what it is and how it works under the hood.

2.    Critical rendering path

3.    RAF

4.    Function patterns: callback, memo, currying, chaining, IIFE, pipe

5.    How to create private property in js class

6.    Private property using WeakMap pattern

7.    Basics about drag/drop api