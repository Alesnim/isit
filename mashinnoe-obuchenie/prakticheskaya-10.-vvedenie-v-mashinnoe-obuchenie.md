---
description: 'Цель работы: ознакомится с типами задач для алгоритмов машинного обучения'
---

# Практическая 10. Введение в машинное обучение

## Теоретические сведения

### Знакомство с линейной алгеброй

В машинном обучении широко используется понятие признака. 

{% hint style="info" %}
**Признаком** называется отображение из множества объектов в множество допустимых значений этого признака. 
{% endhint %}

Если задано множество объектов и некоторый набор признаков, для каждого объекта можно построить его признаковое описание — вектор, составленный из значений этого набора признаков на данном объекте. 

Пусть, например, для каждого магазина торговой сети требуется предсказать прибыль в следующем месяце. Эта задача анализа данных имеет огромную практическую ценность. Действительно, если будет выяснено, что прибыль некоторого магазина упадет, можно будет заблаговременно принять меры по предотвращению этого. В этой задаче множеством объектов является множество магазинов. В качестве признаков разумно выбрать следующие:

* Прибыль магазина в каждом из 4-ех последних месяцев \(4 признака\)
* Планируемое число акций для каждой из трех основных категорий \(3 признака\)
* Географические координаты магазина: широта и долгота \(2 признака\)
* Число дней, когда магазин будет открыт в ближайшем месяце. \(1 признак\)

Признаковым описанием магазина будет вектор, в котором находятся значения данных 10 признаков для данного конкретного магазина. 

Если необходимо работать с признаковыми описаниями сразу нескольких объектов, удобно ввести двумерную структуру данных — матрицу, в которой каждая строка соответствует одному объекту, а каждый столбец — признаку. Работать с векторами и матрицами позволяет аппарат линейной алгебры.

**Векторное пространство** $$V$$ представляет собой набор элементов, называемых векторами, для которых определены операции сложения друг с другом и умножения на скаляр, причем эти операции замкнуты и подчинены восьми аксиомам:

* Коммутативность сложения 
* Ассоциативность сложения 
* Существование нейтрального элемента относительно сложения 
* Существование для каждого вектора x противоположенного вектора $$-x$$ 
* Ассоциативность умножения на скаляр
* Унитарность: умножение на единичный скаляр не меняет вектор
* Дистрибутивность умножения на вектор относительно сложения скаляров
* Дистрибутивность умножения на скаляр относительно сложения векторов

#### Линейная независимость

Линейная зависимость является одним из основополагающих понятий линейной алгебры. Конечный набор элементов векторного пространства называется линейно зависимым, если существует нетривиальная линейная комбинация элементов из этого набора, равная нулевому элементу. Линейная комбинация называется тривиальной, если все коэффициенты в ней равны нулю.

Оказывается, что конечный набор элементов векторного пространства линейно зависим тогда и только тогда, когда один из элементов этого набора может быть выражен через оставшиеся. 

С помощью понятия линейной независимости вводится понятие размерности векторного пространства. А именно: **размерностью** $$dimV$$ векторного пространства $$V$$ называется максимальное число линейно независимых векторов в нем.

Пусть дан некоторый набор объектов $$X$$ и набор $$f_j : X \to \mathbb{R} $$ вещественнозначных признаков. В этом случае набор векторов признаков может быть линейно зависим. Например, признаки вес товара на первом складе, вес товара на втором складе и вес товара на обоих складах линейно зависимы. Другой случай — два вещественнозначных признака отличаются множителем, например являются одной и той же величиной в разных единицах измерения. В обоих случаях наблюдается избыточность информации.

Такая избыточность приводит к дополнительным затратам ресурсов. Более того, линейная зависимость векторов признаков приводит к возникновению проблем при обучении линейной регрессионной модели — об этом пойдет речь в следующем курсе.

Чтобы проверить, являются ли система векторов линейно зависимой, можно составить из них матрицу и вычислить ее ранг. Об этом будет рассказано далее.

#### Нормирование пространства

Для обобщения понятия длины вектора используется понятие нормы. Функция $$\| \cdot \| : V \to \mathbb{R} $$ называется нормой в векторном пространстве $$V$$, если для нее выполняются аксиомы нормы:

1. $$\| x \| = 0 \Leftrightarrow x = 0$$ kxk = 0 ⇐⇒ x = 0 \(Нулевую норму имеет только нулевой вектор\)
2.  $$\forall x, y \in L : \| x + y \| \le \| x \| + \| y \|$$ ∀x, y ∈ L : kx + yk ≤ kxk + kyk \(Неравенство треугольника\)
3. $$\forall \alpha \in  \mathbb{R}, \forall x \in V : \|\alpha x \| = |\alpha| \|x \|$$ \(Условие однородности\)

Пространство с введенной на нем нормой называют нормированным пространством. Обычно используется Евклидова норма $$\| x \| _2$$, другой пример нормы — Манхэттенская норма $$\| x \| _1$$:

$$
\| x \|_2 = \sqrt{\sum_{i = 1}^n x_i^2} \qquad 
\|x\|_1 =  \sum_{i = 1}^n \| x_i \|
$$

#### Метрические пространства

Понятие **расстояние** обобщается с помощью понятия метрики. Пусть $$X$$ — некоторое множество, а числовая функция $$d : X × X \to  \mathbb{R}$$ , которая называется метрикой, удовлетворяет следующим условиям:

1. $$d(x, y) = 0 \Leftrightarrow x =y $$ \(аксиома тождества\).
2. $$d(x, y) = d(x,y)$$\(аксиома симметрии\).
3. $$d(x,y) \le d(x,y) + d(y,z)$$ \(неравенство треугольника\).

Любое нормированное пространство можно превратить в метрическое, определив функцию расстояния $$d(x,y) = \| y - x \|$$. Например, Евклидова и Манхэттенская метрики имеют вид:

$$
p_2(x, y) = \sqrt{\sum_{i=1}^n (x_i - y_i)^2}
\qquad
p_1(x,y) = \sum_{i=1}^n | x_i - y_i |
$$

Название "манхэттенская метрика" связано с уличной планировкой Манхэттена.

#### Скалярное произведение

Скалярным произведением называется функция $$ \langle x, y \rangle : V × V \to \mathbb{R}$$ , удовлетворяющая следующим условиям:

1. $$\langle \alpha x_1 + \beta x_2, y \rangle = \alpha \langle x_1, y \rangle + \langle \beta x_2, y \rangle ;   \quad \forall \alpha, \beta \in  \mathbb{R},  \forall x_1, x_2, y \in V$$
2.  $$\langle y , x \rangle = \langle x, y \rangle ; \quad \forall x,y \in V$$
3.  $$\langle x , x \rangle > 0; \quad \forall x \in V ; \quad \langle 0,0 \rangle = 0$$ 

В современном аксиоматическом подходе уже на основе понятия скалярного произведения векторов вводятся следующие производные понятия:

1. Длина вектора  $$| x|  = \sqrt{\langle x,x \rangle}$$
2. Угол между векторами $$\alpha = arccos \frac{\langle a, b \rangle}{\sqrt{\langle a, a \rangle \langle b,b \rangle}}$$ 

В случае Евклидового пространства скалярное произведение задается формулой $$\langle a, b \rangle  = \sum_{i=1}^n a_i b_i$$ и можно убедиться, что такое определение согласуется с введенной ранее Евклидовой нормой:

$$
\| x \| = \sqrt{\langle x , x \rangle} = \sqrt{\sum_{i= 1}^n x_i^2} = \| x_2 \|
$$

#### Матрицы

{% hint style="info" %}
**Матрицей** размера $$n \times m$$ называется прямоугольная таблица специального вида, состоящая из $$n$$ строк и $$m$$столбцов, заполненная числами.
{% endhint %}

Матрица обычно обозначаются заглавными буквами латинского алфавита, например $$A$$. Элементы матрицы A обозначаются $$a_{ij}$$ , где $$i$$ и $$j$$ — номер строки и столбца, где расположен этот элемент, соответственно. Пространство матриц $$n \times m$$ обозначается $$\mathbb{R}^{n \times m}$$.

Матрицы можно использовать для работы с системами линейных алгебраических уравнений. Например, в задачах линейной классификации решается система линейных алгебраических уравнений с матрицей объектпризнак относительно вектора неизвестных параметров. При этом получившаяся система уравнений может как иметь бесконечное число решении, так и не иметь решений вовсе. Подробнее эти вопросы будут обсуждаться в курсе по машинному обучению.

Для матриц размера $$m \times n $$ результат операции умножения на вектор-столбец размера $$n$$ \(т.е. на матрицу размера $$n \times 1$$ \) есть новый вектор-столбец размера $$m$$:

$$
A_w = 
\begin{pmatrix}
   \sum_{i=1}^n a_{1i}w_i\\
    \sum_{i=1}^n a_{2i}w_i\\
    ... \\
   \sum_{i=1}^n a_{mi}w_i
  \end{pmatrix}
$$

Другими словами, можно сказать, что матрица задает линейное отображение. Системы линейных уравнений лаконично записываются с помощью матриц, например:

$$
\begin{cases} 
12w_1 + 7w_2 + 21w_3 + 31w_4 + 11w_5 = 1 \\
45w_1 − 2w_2 + 14w_3 + 27w_4 + 19w_5 = 0 \\
−3w_1 + 15w_2 + 36w_3 + 71w_4 + 21w_5 = 0 \\
4w_1 − 13w_2 + 55w_3 + 34w_4 + 15w_5 = 1
\end{cases}
$$

в матричной записи имеет вид:

$$
\begin{pmatrix}
12 \; 7\; 21 \; 31\; 11 \\
45 \; −2 \;14 \;27\; 19 \\
−3 \; 15\; 36\; 71\; 21 \\
4 \; −13\; 55\; 34\; 15  
\end{pmatrix}
\cdot 
\begin{pmatrix}
w_1 \\
w_2 \\
w_3 \\ 
w_4 \\
w_5 
\end{pmatrix}
= 
\begin{pmatrix}
1 \\ 0 \\ 0 \\ 1
\end{pmatrix}
$$

#### Понятие собственного вектора

Важной характеристикой матрицы, а также линейного преобразования, заданного этой матрицей, является спектр — набор собственных векторов и соответствующих собственных значений. 

Собственным вектором линейного преобразования $$A$$ называется такой ненулевой вектор $$x \in V$$ , что для некоторого $$\lambda \in  \mathbb{R}$$ выполняется $$Ax = \lambda x$$. Линейное преобразование может как не иметь собственных векторов вообще, например поворот в двумерном пространстве \(кроме нескольких исключительных случаев\), или иметь n собственных векторов с различными собственными значениями. Вопросы существования собственных векторов преобразования разбираются в курсе линейной алгебры. 

Понятие собственного вектора используется в Методе Главных Компонент, который предназначен для уменьшения размерности данных с потерей наименьшего количества информации.

### Задачи оптимизации в Scilab

В качестве простейшей оптимизационной задачи рассмотрим поиск локального минимума функции одной переменной.

$$
f(x) = x^4 + 3x^3 -13x^2 -6x + 26
$$

Решение задачи начнем с построения графика функции \(рис. 1\):

```text
x=-5:0.1:1;
y=x.^4+3*x.^3-13*x.^2-6*x+26;
plot(x,y);
xtitle("График функции f(x)=x^4+3*x^3-13*x^2-6*x+26","X","Y");
xgrid();
```

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 1 - &#x413;&#x440;&#x430;&#x444;&#x438;&#x43A; &#x444;&#x443;&#x43D;&#x43A;&#x446;&#x438;&#x438;](../.gitbook/assets/image%20%2854%29.png)

Из графика видно, что функция имеет минимум в районе точки -4. Для нахождения более точного значения минимума функции в Scilab служит функция `[f,xopt]=optim(costf,x0)`, которая предназначена для поиска минимума любой функции, $$x_0$$ — вектор-столбец начальных приближений длиной $$n$$ , функция `costf` определяет функцию, минимум которой ищется. Функция возвращает минимум функции $$(f)$$ и точку, в которой функция достигает этого значения `(xopt)`.

Главной особенностью функции optim является структура функции `costf`, которая должна быть следующей:

```text
function [f,g,ind]=costf(x,ind)
   //Функция costf должна возвращать функцию f, ее градиент g.
   //f - функция от вектора неизвестных х, минимум которой ищется f=gg(x);
   //g - градиент функции f (вектор частной производной f по x), g=numdiff(gg,x);
endfunction
```

Для функции одной переменной в качестве `f` возвращается функция, минимум которой ищется, в качестве функции `g`— ее производная. Если возвращаемое сформированной функцией `costf` значение ind равно 2, 3 или 4, то функция `costf` обеспечивает поиск минимума, т. е. в качестве результата функции `optim` возвращается `f` и `xopt`. Если `ind=1`, то в функциии `optim` ничего не считается, условие `ind<0` означает, что минимум $$f(x)$$ не может быть оценен, а ind=0 прерывает оптимизацию.

Вообще говоря, значение параметра `ind` является внутренним параметром для связи между `optim` и `costf`, для использования `optim` необходимо помнить, что параметр `ind` должен быть определен в функции `costf`. Таким образом, при использовании функции `optim` необходимо сформировать функцию `costf`, которая должна возвращать минимизируемую функцию `f` и ее градиент \(производную\).

На листинге представлено использование optim для поиска минимума функции:

```text
function [f,g,ind]=fi(x,ind) //Функция fi, в которой будет формироваться функция f и ее производная g.
   f=x^4+3*x^3-13*x^2-6*x+26 //Функция f, минимум которой ищется.
   g=4*x^3+9*x^2-26*x-6 //Функция g - производная от функции f.
endfunction

y0=-2; //Начальное приближение точки минимума.
[fmin,xmin]=optim(fi,y0); //Для поиска точки минимума (xmin) и значения функции (fmin) в ней - вызов функции optim.

```

### Работа с матрицами в Scilab

Самый простой способ задать одномерный массив в Scilab имеет вид:

```text
[name] = Xn:dX:Xk
```

где `name` - имя переменной в которую будет записан сформированный массив `Xn` значение первого элемента массива , `Xk` значение последнего элемента массива `dX`, шаг с помощью которого формируется каждый следующий элемент массива, то есть значение, второго элемента составит`Xn+dX`, третьего `Xn+ dX+dX` и так далее до `Xk`.

Если параметр `dX` в конструкции отсутствует это означает что по умолчанию он принимает значение равное единице, то есть каждый следующий элемент массива равен значению предыдущего плюс один:

```text
[name] = Xn:Xk
```

Переменную заданную как массив можно использовать в арифметических выражениях и в качестве аргумента математических функций Результатом работы таких операторов являются массивы:

```text
Xn=-3.5;
dX=1.5;
Xk=4.5;
X=Xn:dX:Xk
// выведет
// X =
// -3.5000 -2.0000 -0.5000 1.0000 2.5000 4.0000

```

```text
 A=0:5
 // выведет
 // A = 
 // 0 1 2 3 4 5
```

Еще один способ задания векторов и матриц в это их Scilab поэлементный ввод. 

Так для определения _вектор строки_ , следует ввести имя массива а затем после знака присваивания, в квадратных скобках через пробел или запятую перечислить элементы массива:

```text
[name]=x1 x2 … xn // или [name]=x1, x2, …, xn
```

Элементы вектора столбца вводятся через точку с запятой:

```text
[name]=x1; x2; …; xn
```

```text
 X=[1;2;3]
 // выведет
 // X = 
 // 1
 // 2
 // 3
```

Обратиться к элементу вектора можно, указав имя массива и порядковый номер элемента в круглых скобках:

```text
name(index)
```

```text
 W=[1.1,2.3,-0.1,5.88];
 W(1)+2*W(3) // W(1) = 1.1 W(3) = -0.1
```

Ввод элементов матрицы так же осуществляется в квадратных скобках, при этом элементы строки отделяются друг от друга пробелом или запятой, а строки разделяются между собой точкой с запятой:

```text
[name]=[x11, x12, …, x1n; x21, x22, …, x2n;…; xm1, xm2, …, xmn;
```

Обратиться к элементу матрицы можно указав после имени матрицы, в круглых скобках, через запятую, номер строки и номер столбца на пересечении которых элемент расположен:

```text
name(индекс1, индекс2)
```

Далее приведен пример задания матрицы и обращение к ее элементам:

```text
 A=[1 2 3;4 5 6;7 8 9]
 A(1,1) // = 1
 A(3,3) // = 9 
```

Кроме того, матрицы и векторы можно формировать, составляя их из ранее заданных матриц и векторов:

```text
v1=[1 2 3];
v2=[4 5 6]; 
v3=[7 8 9];
V=[v1 v2 v3]
// V =
// 1 2 3 4 5 6 7 8 9 
```

Важную роль при работе с матрицами играет знак двоеточия «:». Указывая его вместо  индекса при обращении к массиву, можно иметь доступ к группам его элементов Например:

```text
 A=[5 7 6 5; 7 10 8 7;6 8 10 9;5 7 9 10]
 A(:,2)
 // 7
 // 10
 // 8
 // 7
```

```text
A=[5 7 6 5; 7 10 8 7;6 8 10 9;5 7 9 10]
A(3,:)
// 6 8 10 9
```

```text
A=[5 7 6 5; 7 10 8 7;6 8 10 9;5 7 9 10]
M=A(3:4,2:3)
// M = 
// 8 10
// 7 9 

// Удалить из матрицы А второй столбец
A(:,2)=[]
// A =
// 5 8 10
// 7 7 9
// 6 10 9
// 5 9 10

//Представить матрицу М в виде вектора–столбца
 v=M(:)
 // v = 
 // 8
 // 7 
 // 10
 // 9
```

#### Дейсвия над матрицами в Scilab

```text
A=[1 2 0;-1 3 1;4 -2 5];
B=[-1 0 1;2 1 1;3 -1 -1];
//Вычислить (AT+B)2 - 2A(0.5BT-A)
(A'+B)^2-2*A*(1/2*B'-A)
// выведет
// 10. 8. 24.
// 11. 20. 35.
// 63. - 30. 68.
//Решить матричные уравнения А∙Х=В и Х∙A=B.
A=[3 2;4 3];
B=[-1 7;3 5];
//Решение матричного уравнения AX=B:
X=A\B
// X =
// - 9. 11.
// 13. - 13.
//Решение матричного уравнения XA=B:
X=B/A
// X =
// - 31. 23.
// - 11. 9.
//Проверка
X*A-B
// выведет
// 0. 0.
// 0. 0.
```

Кроме того если к некоторому заданному вектору или матрице применить математическую функцию, то результатом будет новый вектор или матрица той же размерности, но элементы будут преобразованы в соответствии с заданной функцией:

```text
x=[0.1 -2.2 3.14 0 -1];
sin(x)
// выведет
// 0.0998 -0.8085 0.0016 0 -0.8415
```

Для работы с матрицами и векторами в существуют специальные функции Scilab . Рассмотрим наиболее часто используемые из них:

* `matrix(A [,n,m])` преобразует матрицу A в матрицу другого размера;
* `ones(m,n)` ****создает матрицу единиц из m строк и n столбцов;
* `zeros(m,n)` создает нулевую матрицу из m строк и n столбцов;
* `eye(m,n)`формирует единичную матрицу из m строк и n столбцов;
* `rand(n1,n2,…nn[,fl])`формирует многомерную матрицу случайных чисел, необязательный параметр `p`, это символьная переменная с помощью которой можно задать тип распределения случайной величины \('uniform' равномерное, 'normal' гауссовское\);  `rand(m,n)`формирует матрицу m на n случайных чисел;  `rand(M)`формирует матрицу случайных чисел, размер которой совпадает с размером матрицы М;  `rand()` случайное скалярное число;
* `sparse([i1 j1;i2 j2;…;in jn],[n1,n2,…,nn])`формирует разреженную матрицу; для создания матрицы такого типа необходимо указать индексы ее ненулевых элементов `[i1 j1,i2 j2,…,in jn]`и их значения `[n1,n2,…,nn]`, индексы одного элемента отделяются друг от друга либо пробелом, либо запятой а пары индексов соответственно точкой с запятой значения элементов разделяются запятыми; при попытке просмотреть матрицу подобного типа пользователю будет предоставлено сообщение о ее размерности, а так же значения ненулевых элементов и их местоположение в матрице;
* `full(M)`вывод разреженной матрицы М в виде таблицы;
* `det(M)`вычисляет определитель квадратной матрицы М;
* `rank(M[,tol])` вычисление ранга матрицы M с точностью `tol`
* `spec(M)`вычисляет собственные значения и собственные векторы квадратной матрицы M;
* `inv(A)` вычисляет матрицу обратную к A;
* `linsolve(A,b)` решает систему линейных алгебраических уравнений вида $$A_1x_1 + A_2x_2 + ... + A_nx_n + b = 0 $$
* `rref(A)`осуществляет приведение матрицы A , к треугольной форме используя метод Гаусса;

## Ход работы

### Задание 1. Оптимизация функций в Scilab

{% hint style="info" %}
Функция optim ожидает на вход функцию возвращающую несколько значений: значение функции в точке $$f$$ , градиент функции $$g$$ и параметр оптимизации $$ind$$ 
{% endhint %}

1. Прочесть справку про функциям `optim` ,  `fminsearch`
2. Найти оптимум функции: $$f(x) = a + bx + cx^2 + dx^3$$ при  $$x \in [-10, 53]$$

| № | a | b | c | d |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 20 | 3 | -40 | 1 |
| 2 | 30 | -50 | -55 | 3 |
| 3 |  10 | -20 | -40 | 1 |
| 4 |  2 | -5 | 47 | -3 |
| 5 |  4 | -5 | -26 | 2 |
| 6 | 50 | -63 | -25 | 1 |
| 7 | 23 | -80 | -64 | 5 |
| 8 | 12 | -8 | -40 | 3 |
| 9 | 14 | 2 | -26 | 1 |
| 10 | 26 | -86 | -59 | 3 |
| 11 | 44 | 3 | -63 | 1 |
| 12 | 71 | 3 | -120 | 2 |
| 13 | 62 | -1 | -86 | 2 |
| 14 | 48 | -38 | -71 | 5 |
| 15 | 39 | -96 | -67 | 4 |

### Задача 2. Работа с матрицами

1. Решить СЛАУ при помощи [метода Крамера](https://ru.wikipedia.org/wiki/%D0%9C%D0%B5%D1%82%D0%BE%D0%B4_%D0%9A%D1%80%D0%B0%D0%BC%D0%B5%D1%80%D0%B0):

| № | $$x_1$$  | $$x_2$$  | $$x_3$$  | $$x_4$$  | $$x_5$$  | b |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 2 | 1 | -5 | 4 | -8 | 32 |
| 2 | 5 | -12 | 8 | 4 | 0 | 0 |
| 3 | 3 | 2 | 5 | -2 | 17 | 9 |
| 4 | 0 | 2 | -1 | 2 | 2 | 14 |

2. Решить СЛАУ при помощи [метода обратной матрицы](http://cyclowiki.org/wiki/%D0%9C%D0%B5%D1%82%D0%BE%D0%B4_%D0%BE%D0%B1%D1%80%D0%B0%D1%82%D0%BD%D0%BE%D0%B9_%D0%BC%D0%B0%D1%82%D1%80%D0%B8%D1%86%D1%8B#:~:text=%D0%9C%D0%B5%D1%82%D0%BE%D0%B4%20%D0%BE%D0%B1%D1%80%D0%B0%D1%82%D0%BD%D0%BE%D0%B9%20%D0%BC%D0%B0%D1%82%D1%80%D0%B8%D1%86%D1%8B%20%E2%80%94%20%D1%8D%D1%82%D0%BE%20%D1%81%D0%BF%D0%BE%D1%81%D0%BE%D0%B1,%D0%BC%D0%B0%D1%82%D1%80%D0%B8%D1%86%D0%B0%20%28%D0%BA%20%D0%BC%D0%B0%D1%82%D1%80%D0%B8%D1%86%D0%B5%20A%29.):

| № | $$x_1$$  | $$x_2$$  | $$x_3$$  | $$x_4$$  | b |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 5 | 8 | -18 | 4 | 8 |
| 2 | 4 | 7 | 12 | 9 | 0 |
| 3 | 1 | 1 | 1 | 1 | 1 |
| 4 | 2 | 7 | 2 | 3 | 10 |

## Контрольные вопросы

1. Дайте определение понятию собственный вектор
2. Что такое признак
3. Дайте определение понятию нормирование
4. Что такое векторное пространство
5. Что такое пространство признаков

### Критерии оценки практического занятия

Оценивается знание материала, способность к его обобщению, критическому осмыслению, систематизации. 

* 3 балла: студент полностью выполнил задания.
* 2 балла: в усвоении учебного материала допущены небольшие пробелы.
* 1 балл: неполно или непоследовательно реализовано задание.
* 0 баллов: не раскрыто основное содержание учебного материала.

**Максимальный балл: 3 балла**
