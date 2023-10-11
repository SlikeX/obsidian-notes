![[presentation-angular-final.jpg]]

# Novice

-   Typescript(types, Classes, Interfaces, Decorators, any, compile time checks understanding, runtime result)
-   Components (Properties, Inputs, Outputs, Attributes Bindings)
-   LifeCycle hooks(OnInit, OnDestroy, OnChanges)
-   Templates (Scope, Interpolation, component interaction)
-   Directives (Build-In ones, custom Attribute directive) +-
-   Pipes(Pure, Impure)
-   Dependency Injection (usage)
-   NgModules (declarations, imports, exports)
-   Forms(main directives, usage) -
-   Rxjs(Observable, Observer, switchMap, map, tap, subscribe)
-   ServicesUnit Tests (TestBed, Jasmine)

# Intermediate

-   Typescript (object, never, void, union, intersection, basic generic types)
-   LifeCycle hooks (AfterContentInit, AfterViewInit)
-   Components (ViewEncapsulation)
-   Change Detection (Strategy, NgZone, ChangeDetectorRef, OnPush)
-   Dependency Injection (Extended providers config, Hierarchical injectors)
-   Http (HttpClient, Interceptors)
-   Forms (Validation, Value Accessors)
-   Routing (Resolve, Guards, Data, pathMatch, ActivatedRoute)
-   Component Nesting (ng-content, ViewChild, ContentChild)
-   Unit Tests (TestHostComponent)
-   Rxjs (hot vs cold, concatMap, exhaustMap, mergeMap, zip, combineLatest, scan)
-   Dynamic Components
-   State Management (NgRx, NgXs, Akita)

# Advanced

-   Typescript (type guard, advanced generics).
-   Change Detection (tick(), runOutsideAngular, expressionChangedError).
-   Dependency Injection (Lazy module injectors, viewProviders, decorators, multi provider).
-   Forms (Custom Value Accessors).
-   Directives (ng-template, templateContext, embeddedView, Renderer, microsyntax).
-   LifeCycle hooks (ngDoCheck, ngAfterContentChecked, ngAfterViewChecked).
-   Rxjs (schedulers, multicasting, share, expand, custom operator).
-   Angular CompilerAnimation (Query, Trigger, Stagger).
-   Ng CLI.
-   Internationalization.
-   Routing (RouteReuseStrategy, PreloadingStrategy, router events,multi-outlet).
-   Server-Side Rendering.
-   Service/Web Workers.


# Novice

## *Typescript

##### Декраторы

*Декораторы* - это функция, которая добавляет определеные метаданные(свойства, методы и т.п) объектам, которые он декорирует. Декоратор можно применять к следующим объектам: 
Класс
Метод
Геттер/сеттер
Свойство
Аргумент/параметр

В зависимости от того, к чему мы хотим применить декоратор, данная функция будет иметь разные сигнатуры, которые заранее определены и если мы хотим добавить дополнительные параметры, аргументы, конфигурационные объекты, то необходимо использовать замыкание внутри функции декоратора.![[Pasted image 20230503094233.png]]
тут мы возвращаем функцию-декоратор, и благодаря замыканию мы имеем доступ к параметру value.

При использовании нескольких декораторов подряд их фабричные функции выполняются сверху вниз, а сами декораторы снизу вверх.
![[Pasted image 20230503094612.png]]![[Pasted image 20230503094620.png]]

##### Templates scope

Под scope в темплейте поразумевается объект, на который можно сосласть при помощью this. this в темплейте является экземпляр контроллера, т.е если в контроллере есть свойсво message, то до него можно достучаться в темплейте через this.message![[Pasted image 20230504124508.png]]
![[Pasted image 20230517143511.png]]