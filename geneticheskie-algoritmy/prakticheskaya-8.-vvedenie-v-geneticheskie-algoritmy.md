---
description: 'Цель работы: ознакомится с применением и устройством генетических алгоритмов'
---

# Практическая 8. Введение в генетические алгоритмы

## Теоретические сведения

Генетические алгоритмы относят к области мягких вычислений. Термин «мягкие вычисления» введен Лофти Заде в 1994 году. Это понятие объединяет такие области, как нечеткая логика, нейронные сети, вероятностные рассуждения, сети доверия1 и эволюционные алгоритмы, которые дополняют друг друга и используются в различных комбинациях или самостоятельно для создания гибридных интеллектуальных систем. Первая схема генетического алгоритма была предложена в 1975 году в Мичиганском университете Джоном Холландом \(John Holland\), а предпосылками этому послужили работы Ч. Дарвина \(теория эволюции\) и исследования Л.Дж.Фогеля, А.Дж. Оуэнса, М.Дж.Волша по эволюции простых автоматов, предсказывающих символы в цифровых последовательностях \(1966\).

Новый алгоритм получил название «репродуктивный план Холланда» и в дальнейшем активно использовался в качестве базового алгоритма в эволюционных вычислениях. Идеи Холланда развили его ученики Кеннет Де Йонг \(Kenneth De Jong\) из университета Джорджа Мейсона \(Вирджиния\) и Дэвид Голдберг \(David E. Goldberg\) из лаборатории ГА Иллинойса. Благодаря им, был создан классический ГА, описаны все операторы и исследовано поведение группы тестовых функций \(именно алгоритм Голдберга и получил название «генетический алгоритм»\). 

{% hint style="info" %}
 **Генетический алгоритм** \(англ. genetic algorithm\) — это эвристический алгоритм поиска, используемый для решения задач оптимизации и моделирования путём последовательного подбора, комбинирования и вариации искомых параметров с использованием механизмов, напоминающих биологическую эволюцию.
{% endhint %}

### Простой пример генетического алгоритма

Рассмотрим принципы работы генетических алгоритмов на максимально простом примере. Пусть требуется найти глобальный минимум функции:

$$
y(x) = 5 -24x + 17x^2 - \frac{11}{3}x^3 + \frac{1}{4}x^4
$$

на отрезке \[0; 7\] \(рис. 1\). На этом отрезке функция принимает минимальное значение в точке $$x = 1$$ . Очевидно, что в точке  функция попадает в локальный минимум. Если для нахождения глобального минимума использовать градиентные методы, то в зависимости от начального приближения можно попасть в данный локальный минимум.

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 1 - &#x413;&#x440;&#x430;&#x444;&#x438;&#x43A; &#x444;&#x443;&#x43D;&#x43A;&#x446;&#x438;&#x438;](../.gitbook/assets/image%20%2845%29.png)

Рассмотрим на примере данной задачи принцип работы генетических алгоритмов. Для простоты положим, что x принимает лишь целые значения, т.е. $$x \in \{0, 1, 2, 3, 4, 5, 6, 7 \}$$. Это предположение существенно упростит изложение, сохранив все основные особенности работы генетического алгоритма. 

Выберем случайным образом несколько чисел на отрезке $$[0; 7]: \{2, 3, 5, 4 \}$$. Будем рассматривать эти числа в качестве пробных решений нашей задачи.

Основной идеей генетических алгоритмов является организация «борьбы за существование» и «естественного отбора» среди этих пробных решений. Запишем пробные решения в двоичной форме: **{010, 011, 101, 100}**. Поскольку генетические алгоритмы используют биологические аналогии, то и применяющаяся терминология напоминает биологическую. 

Так, одно пробное решение, записанное в двоичной форме, мы будем называть особью или _**хромосомой**_, а набор всех пробных решений – _**популяцией**_. Как известно, принцип естественного отбора заключается в том, что в конкурентной борьбе выживает наиболее приспособленный. В нашем случае приспособленность особи определяется целевой функцией: чем меньше значение целевой функции, тем более приспособленной является особь, т.е. пробное решение, использовавшееся в качестве аргумента целевой функции \(см. табл. 1\).

Теперь приступим к процессу _**размножения**_: попробуем на основе исходной популяции создать новую, так чтобы пробные решения в новой популяции были бы ближе к искомому глобальному минимуму целевой функции. Для этого сформируем из исходной популяции брачные пары для скрещивания. Поставим в соответствие каждой особи исходной популяции случайное целое число из диапазона от 1 до 4. Будем рассматривать эти числа как номера членов популяции. При таком выборе какие-то из членов популяции не будут участвовать в процессе размножения, так как образуют пару сами с собой. Какие-то члены популяции примут участие в процессе размножения неоднократно с различными особями популяции. Процесс размножения \(_рекомбинация_\) заключается в обмене участками хромосом между родителями. Например, пусть скрещиваются две хромосомы **111111** и **000000**. Определяем случайным образом точку разрыва хромосомы, пусть, это будет 3: **111\|111** и **000\|000**. Теперь хромосомы обмениваются частями, стоящими после точки разрыва, и образуют двух новых потомков: **111000** и **000111**.

#### Таблица 1

| № | Целое число | Двоичное число | Приспособленость |
| :--- | :--- | :---: | :---: |
| 1 | 2 | 010 | -0,33 |
| 2 | 3 | 011 | 7,25 |
| 3 | 5 | 101 | 7,92 |
| 4 | 4 | 100 | 10,33 |

Для нашей популяции процесс создания первого поколения потомков показан в таблице 2.

{% hint style="info" %}
**Точка кроссинговера** - точка внутри хромосомы, в которой обе хромосомы делятся на две части и обмениваются ими
{% endhint %}

#### Таблица 2

| № | Особь популяции | Выбранный номер | Вторая выбранная особь | Точка кроссинговера | Особи-потомки |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 010 | 1 | 010 | 1 | 000 |
| 2 | 011 | 4 | 100 | 1 | 110 |
| 3 | 101 | 3 | 101 | 2 | 100 |
| 4 | 100 | 1 | 010 | 2 | 011 |

Следующим шагом в работе генетического алгоритма являются мутации, т.е. случайные изменения полученных в результате скрещивания хромосом. Пусть вероятность мутации равна 0,3. Для каждого потомка возьмем случайное число на отрезке $$[0; 1] $$, и если это число меньше 0,3, то инвертируем случайно выбранный ген \(заменим 0 на 1 или наоборот\) \(см. табл. 3\).

#### Таблица 3

ОП - особи-потомки;

СЧ - случайное число;

ВГ - выбранный ген;

ППМ - потомок после мутации;

ПДМ - потомок до мутации;

ППоМ - приспособленность после мутации.

| № | ОП | СЧ | ВГ | ППМ | ПДМ | ППоМ |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 000 | 0,1 | 3 | 001 | 5 | -5,42 |
| 2 | 110 | 0,6 | - | 110 | 5 | 5 |
| 3 | 100 | 0,5 | - | 100 | 10,33 | 10,33 |
| 4 | 011 | 0,2 | 1 | 111 | 7,25 | 12,58 |

Как видно на примере, мутации способны улучшить \(первый потомок\) или ухудшить \(четвертый потомок\) приспособленность особи-потомка. В результате скрещивания хромосомы обмениваются «хвостами», т.е. младшими разрядами в двоичном представлении числа. В результате мутаций изменению может подвергнуться любой разряд, в том числе, старший. Таким образом, если скрещивание приводит к относительно небольшим изменениям пробных решений, то мутации могут привести к существенным изменениям значений пробных решений \(см. рис. 2\). Теперь из четырех особей-родителей и четырех полученных особей потомков необходимо сформировать новую популяцию. В новую популяцию отберем четыре наиболее приспособленных особей из числа «старых» особей и особей-потомков \(см. табл. 4\). В результате получим новое поколение, которое представлено на рис. 3. 

Получившуюся популяцию можно будет вновь подвергнуть кроссинговеру, мутации и отбору особей в новое поколение. Таким образом, через несколько поколений мы получим популяцию из похожих и наиболее приспособленных особей. Значение приспособленности наиболее «хорошей» особи \(или средняя приспособленность по популяции\) и будет являться решением нашей задачи. Следуя этому, в данном случае, взяв наиболее приспособленную особь **001** во втором поколении, можно сказать, что минимумом целевой функции является значение −5,42, соответствующее аргументу $$x = 1$$. 

Тем самым попадания в локальный минимум удалось избежать! На данном примере разобран вариант простого генетического алгоритма. При дальнейшем использования ГА к разным задачам возможно моделирование основных операторов алгоритма.

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 2 - &#x418;&#x437;&#x43C;&#x435;&#x43D;&#x435;&#x43D;&#x438;&#x435; &#x43F;&#x43E;&#x43F;&#x443;&#x43B;&#x44F;&#x446;&#x438;&#x438; &#x432;&#x43E; &#x432;&#x440;&#x435;&#x43C;&#x44F; &#x435;&#x441;&#x442;&#x435;&#x441;&#x442;&#x432;&#x435;&#x43D;&#x43D;&#x43E;&#x433;&#x43E; &#x43E;&#x442;&#x431;&#x43E;&#x440;&#x430;](../.gitbook/assets/image%20%2846%29.png)

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 3 -  &#x41C;&#x438;&#x43D;&#x438;&#x43C;&#x438;&#x437;&#x438;&#x440;&#x443;&#x435;&#x43C;&#x430;&#x44F; &#x444;&#x443;&#x43D;&#x43A;&#x446;&#x438;&#x44F; &#x438; &#x43E;&#x441;&#x43E;&#x431;&#x438; &#x43D;&#x43E;&#x432;&#x43E;&#x439; &#x43F;&#x43E;&#x43F;&#x443;&#x43B;&#x44F;&#x446;&#x438;&#x438;](../.gitbook/assets/image%20%2847%29.png)

#### Таблица 4

| № | Особи | Приспособляемость | Новая популяция | Приспособленность в новой популяции  |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 010 | -0,33 | 001 | -5,42 |
| 2 | 011 | 7,25 | 010 | -0,33 |
| 3 | 101 | 7,92 | 110 | 5 |
| 4 | 100 | 10,33 | 011 | 7,25 |
| 5 | 001 | -5.42 | - | - |
| 6 | 110 | 5 | - | - |
| 7 | 100 | 10,33 | - | - |
| 8 | 111 | 12,58 | - | - |


