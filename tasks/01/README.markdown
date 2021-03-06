# Седем малки функции

Първата задача ще бъде да напишете 2 малки функции за намиране на нулите на непрекъснати функции и 5 малки функции за работа с опашки.

## Нула на функция

[Методът на полу-интервалите](http://en.wikipedia.org/wiki/Bisection_method) е прост, но мощен метод за намиране на нулите на непрекъстанти функции.

Първата функция, която трябва да дефинирате е `bisect [f neg-point pos-point close-enough?]`. Тук `f` е функция на един аргумент (число), която връща число и е непрекъсната, a `neg-point` и `pos-point` са точки, където функцията има съответно отрицателна и положителна стойност. `close-enough?` е функция, която приема две числа и връща дали две числа са достатъчно близко едно до друго, за да ги смятаме за равни.

Алгоритъмът е следния: ако `neg-point` и `pos-point` са равни (определено от `close-enough?`), тогава средата между тях е нула на `f`. Иначе разделяме интервала между тях на две и проверяваме дали средната точка не е нула на `f`. Ако не е, тогава по същия метод търсим в половината на интервала, чиито крайни точки имат различни знаци.

Тъй като функцията е непрекъсната, тя винаги има нула в интервала `[neg-point, pos-point]` (анализът отвръща на удара).

Освен `bisect`, трябва да дефинирате и още една, по-удобна функция: `make-bisector [tolerance]`. Тя трябва да връща функция, която приема три аргумента: `[f a b]` и намира на нула на функцията `f` в интервала `[a, b]`. `make-bisect` трябва да ползва `bisect` като за две числа трябва да се смята, че са достатъчно близки, ако разликата им е по-малка от `tolerance`. За разлика от `bisect`, тук не е сигурно в коя от двете точки стойността на `f` е положителна и в коя – отрицателна. Ако и в `a` и в `b` `f` е с еднакъв знак, функцията трябва да върне `nil`.

## Опашка

Останалите функции, които трябва да реализирате са проста опашка:

* `make-queue` трябва да връща празна опашка.
* `push-to-queue [q x]` трябва да върне нова опашка, добавяйки стойността на `x` към `q`.
* `peek-at-queue [q]` трябва да върне елемента на върха на опашката. Ако опашката е празна трябва да върне `nil`.
* `pop-from-queue [q]` трябва да върне нова опашка, като премахне елемента от върха на `q`. Ако опашката е празна трябва да върне празна опашка.
* `empty-queue? [q]` трябва да върне дали опашката е празна или не.

Ако искате да създадете опашка, да добавите в нея `:foo` и `:bar` и след това да извадите първия елемент, това може да стане така:

    (def q1 (make-queue))
    (def q2 (push-to-queue q1 :foo))
    (def q3 (push-to-queue q2 :bar))

    (def first-element (peek-at-queue q3)) ; :foo
    (def final-queue (pop-from-queue q3))  ; Опашка с един елемент - :bar

Обърнете внимание, че не сме задали типа на опашката. Може да я реализирате както искате - вектор, списък или дори `cons` клетки. Ние ще ползваме единствено интерфейса, който сме задали чрез функциите.

Допълнително, може да помислите как да реализирате опашката ефективно. Това не е изискване към задачата, но е добро упражнение.

## Документация

Припомняме ви, че може да разгледате [Clojure cheatsheet](http://clojure.org/cheatsheet) ако се почувстате загубени или документацията в [Clojure Docs](http://clojuredocs.org/quickref/Clojure%20Core), която макар и за Clojure 1.3 е релевантна.
