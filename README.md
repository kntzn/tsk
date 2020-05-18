# tsk
КМБ по Программированию
В этом невероятно продуманном и ни капли не спонтанном курсе молодого бойца по программированию, я планирую научить всех желающих C (а потом и С++) на примере относительно, но все же прикладных задач. Причем я собираюсь каждую неделю усложнять само задание, чтобы вы могли продолжать развивать свою программу, тем самым привыкая писать легко расширяемый код, поскольку в ваших же интересах писать его так, чтобы затем не приходилось переделывать всю программу целиком.

<h1>Задание 1: Конвертер систем счисления</h1>
<h2>Часть 1: Двоично-десятичный код (BCD)</h2>
<h3>Теория</h3>
<h4>Что такое программирование?</h4> Что значит "работать программистом"? По сути, это работа переводчика с одного языка на другой. И это даже не перевод с русского на C++ или python, или любой другой язык программирования. Это перевод со сложного русского, на простой, но оттого и непонятный, язык компьютера/ЭВМ/процессора или чего бы то ни было, что говорит на языке нулей и единиц.

Как и в любом языке, в нем существует минимальная единица - бит. Один бит можно воспринимать как одну букву в нашем человеческом языке. И прежде, чем писать что-то сложное, что-то, возможно, великое, стоит прочувствовать те самые нули и единицы, что были в фильме "Матрица". Научиться видеть в них то, что они из себя представляют, и что в себе несут. И для улучшения понимания стоит попробовать написать перевод привычных нам чисел в 10й системе в мистическую двоичную. Почему двоичную? Потому что название каждой системы счисления несет в себе то, сколько ее минимальная единица (а, проще говоря, цифра) может нести в себе различных значений. Ну, например, для нашей десятичной системы это, как легко догадаться, десять: 

<i>0, 1, 2... 9 - Сосчитали все цифры по пальцам, получили 10, молодцы</i>

И как раз-таки двоичная система и является языком компьютера, ведь каждая цифра несет в себе два значения - 0 и 1. То есть, одна цифра в двоичной системе - это один бит, одна буква на языке компьютера.
<h4>А теперь о главном</h4> 
<i>-Система счисления? Это че ваще такое?</i>
Безусловно, я могу развести здесь теории на пол сайта про то, что это такое. Про то, что они бывают позиционные, непозиционные, и так далее. Но будем реалистами. Все, что нужно для базового понимания происходящего, это обыкновенная позиционная система счисления. И более того, договоримся, что система счисления отныне называется сокращенно "сс".

И что же это такое? Вы удивитесь, но на самом деле, двоичная сс мало отличается от нашей десятичной. Рассмотрим пример, число <b>8715</b>. Что это такое по существу?

<code>
8715 - это восемь тысяч, семь сотен, один десяток и пять единиц
</code>

А теперь по-другому

<code>
8715 - это 8000        + 700       + 10           + 5
</code>

А теперь еще немного по-другому

<code>
8715 - это 8 * 1000    + 7 * 100   + 1 * 10       + 5 * 1
</code>

И еще чуть-чуть

<code>
8715 - это 8 * 10^3    + 7 * 10^2  + 1 * 10^1     + 5 * 1
</code>

И вот мы вычленили все цифры из этого числа: 8, 7, 1, 5

И если на секунду вдуматься, как из четырех цифр, идущих в известной последовательности, мы получаем исходное число, то мы просто считаем, что последняя цифра это число единиц, предпоследняя - это число десятков и так далее.

Единственное, что плохо в нашем примере - это <b> 5 * 1</b>. Эта единица очевидно выбивается из ряда степеней десяток, на которые мы умножаем наши цифры. 

Посмотрим на наш ряд: <b>10^3, 10^2, 10^1, ???</b> 

Напрашивается <b>10^0</b>, не так ли? И, к счастью, <b>10^0 = 1</b>. То есть мы можем переписать наш ряд еще немного:

<code>
8715 - это 8 * 10^3    + 7 * 10^2  + 1 * 10^1     + 5 * 10^0
</code>

И на этой ноте я хочу задать читателю один вопрос, правильный ответ на который сделает для него <b>любую</b> сс одинаково понятной:

<code> А почему в этом примере используются степени десяти? </code>

Потому что это число записано в десятичной сс. *Сейчас самое время пойти заварить чай и осознать всю суть.*

<h4>Смотрим на задачу с другой стороны</h4>
Если вы правильно меня поняли, то вся разница между разными системами счисления заключается в том, какое число будет возводиться в степень. И для двоичной системы это, очевидно, два. Попробуйте это ощутить на таком примере.

<code>1101(2) = 1 * 2^3    +    1 * 2^2  +    0 * 2^1  +    1 * 2^0 = </code>
  
<code>1101(2) = 1 * 8      +    1 * 4    +    0 * 2    +    1 * 1   = </code>

<code>1101(2) = 8          +    4        +    0        +    1       =  13(10)</code>

Напоминаю, в двоичной системе счисления есть только две цифры - 0 и 1. Поэтому числа 1201, например, в двоичной системе быть не может.

Теперь встает важный вопрос: как получить обратный результат? Как из 13(10) можно вообще получить 1101(2)?

На самом деле, идея довольно проста. Рассмотрим последнюю цифру и обратим внимание на ее множитель:

<code> Для любой системы счисления, будь то 10 или 2, 10^0 = 2^0 = 1 </code>

Поэтому последняя цифра в любой системе счисления будет отвечать за число единиц:

<code>
13(10)  % 10 = 3 - число единиц в числе 13 в 10й сс
  
1101(2) % 2  = 1 - число единиц в числе 1101 в 2й сс
</code>

А теперь попробуем скомбинировать два этих факта: 

<code>
13(10)  % 2 = 1 - число единиц в числе 13 в 2й сс
</code>

То есть, последняя цифра числа 13 в 2й сс будет 1. Следующим делом, надо получить следующую. Получить следующую цифру - значит понять, сколько раз уместится 2^1 в числе 13? 

Очевидно, что она уместится <b>13/(2^1) = 6.5 = 6 полных раз</b>. Это значит, что

<code>
13(10)    =    6 * 2^1    +     1 * 2^0, что справедливо
</code>

Но помните, что я говорил, что не может быть других цифр в двоичной системе, кроме 0 и 1? 

Это значит, что от 6 надо избавляться. Как? Переводить ее в двоичную систему, очевидно.

Продолжаем в том же духе, как и с нашим исходным числом:

<code>
6 % 2 = 0 - число единиц в числе 6 в 2й сс
</code>

<code>
6 / 2^1 = 3 - три полных раза 2^1 умещается в 6
</code>

<code>
Это значит, что 6 = 3 * 2^1 + 0 * 2^0
</code>

И теперь фокус, подставим этот результат сюда: <b>13(10)    =    6 * 2^1    +     1 * 2^0</b>

<code>
13(10) = (3 * 2^1 + 0 * 2^0) * 2^1    +     1 * 2^0
</code>

<code>
13(10) = 3 * 2^2 + 0 * 2^1 + 1 * 2^0
</code>

Тройки все еще не может быть в 2й сс. Переводим и её

<code>3 % 2 = 1 - число единиц в числе 3 в 2й сс</code>

<code>3 / 2^1 = 1 - один полный раз 2^1 умещается в 3 </code>

<code> Это значит, что 3 = 1 * 2^1 + 1 * 2^0 </code>

И снова подставляем:

<code> 13(10) = 3 * 2^2 + 0 * 2^1 + 1 * 2^0 </code>

<code> 13(10) = (1 * 2^1 + 1 * 2^0) * 2^2 + 0 * 2^1 + 1 * 2^0 </code>

<code> 13(10) = 1 * 2^3 + 1 * 2^2 + 0 * 2^1 + 1 * 2^0 </code>

И теперь мы можем четко видеть, как появились те самые цифры 1, 1, 0, 1

<h4>Обобщаем механизм перевода</h4>

Итак, теперь я попытаюсь чуть менее строго, но чуть более понятно объяснить, как работают механизмы перевода из 2й в 10ю сс и наоборот.
