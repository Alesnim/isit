---
description: 'Цель работы: изучить работу алгоритмов деревьев решений'
---

# Практическая 14. Деревья решений

## Теоретические сведения

Мы уделили достаточно много внимания линейным методам, которые обладают рядом важных достоинств: быстро обучаются, способны работать с большим количеством объектов и признаков, имеют небольшое количество параметров, легко регуляризуются. При этом у них есть и серьёзный недостаток — они могут восстанавливать только линейные зависимости между целевой переменной и признаками. Конечно, можно добавлять в выборку новые признаки, которые нелинейно зависят от исходных, но этот подход является чисто эвристическим, требует выбора типа нелинейности, а также всё равно ограничивает сложность модели сложностью признаков (например, если признаки квадратичные, то и модель сможет восстанавливать только зависимости второго порядка).

{% hint style="info" %}
Решающими деревьями — семейством моделей, которые позволяют восстанавливать нелинейные зависимости произвольной сложности.
{% endhint %}

Решающие деревья хорошо описывают процесс принятия решения во многих ситуациях. Например, когда клиент приходит в банк и просит выдать ему кредит, то сотрудник банка начинает проверять условия:

1. Какой возраст у клиента? Если меньше 18, то отказываем в кредите, иначе продолжаем.&#x20;
2. Какая зарплата у клиента? Если меньше 50 тысяч рублей, то переходим к шагу 3, иначе к шагу 4.
3. Какой стаж у клиента? Если меньше 10 лет, то не выдаем кредит, иначе выдаем.
4. Есть ли у клиента другие кредиты? Если есть, то отказываем, иначе выдаем.

Такой алгоритм, как и многие другие, очень хорошо описывается решающим деревом. Это отчасти объясняет их популярность.&#x20;

Первые работы по использованию решающих деревьев для анализа данных появились в 60-х годах, и с тех пор несколько десятилетий им уделялось очень большое внимание. Несмотря на свою интерпретируемость и высокую выразительную способность, деревья крайне трудны для оптимизации из-за свой дискретной структуры — дерево нельзя продифференцировать по параметрам и найти с помощью градиентного спуска хотя бы локальный оптимум. Более того, даже число параметров у них не является постоянным и может меняться в зависимости от глубины, выбора критериев дробления и прочих деталей. Из-за этого все методы построения решающих деревьев являются жадными и эвристичными. На сегодняшний день решающие деревья не очень часто используются как отдельные методы классификации или регрессии. В то же время, как оказалось, они очень хорошо объединяются в композиции — решающие леса, которые являются одними из наиболее сильных и универсальных моделей.

### Определение решающего дерева

Рассмотрим бинарное дерево, в котором:

* каждой внутренней вершине $$v$$ приписана функция (или предикат) $$\beta_v : X \to \{ 0, 1\}$$ ;
* каждой листовой вершине $$v$$ приписан прогноз $$c_v ∈ Y$$ (в случае с классификацией листу также может быть приписан вектор вероятностей).

Рассмотрим теперь алгоритм $$a(x)$$, который стартует из корневой вершины $$v_0$$ и вычисляет значение функции $$\beta v_0$$. Если оно равно нулю, то алгоритм переходит в левую дочернюю вершину, иначе в правую, вычисляет значение предиката в новой вершине и делает переход или влево, или вправо. Процесс продолжается, пока не будет достигнута листовая вершина; алгоритм возвращает тот класс, который приписан этой вершине. Такой алгоритм называется _бинарным решающим деревом_.

На практике в большинстве случаев используются одномерные предикаты $$\beta v$$ , которые сравнивают значение одного из признаков с порогом:

$$
\beta_v (x;j,t) = [x_j < t]
$$

Существуют и многомерные предикаты, например:

* &#x20;линейные: $$\beta_v (x) = [\langle w, x\rangle < t]$$&#x20;
* метрические $$\beta_v(x) = [ρ(x, x_v) < t]$$, где точка $$x_v$$ является одним из объектов выборки любой точкой признакового пространства

Многомерные предикаты позволяют строить ещё более сложные разделяющие поверхности, но очень редко используются на практике — например, из-за того, что усиливают и без того выдающиеся способности деревьев к переобучению. Далее мы будем говорить только об одномерных предикатах.

### Построение деревьев

Легко убедиться, что для любой выборки можно построить решающее дерево, не допускающее на ней ни одной ошибки — даже с простыми одномерными предикатами можно сформировать дерево, в каждом листе которого находится ровно по одному объекту выборки. Скорее всего, это дерево будет переобученным и не сможет показать хорошее качество на новых данных. Можно было бы поставить задачу поиска дерева, которое является минимальным (с точки зрения количества листьев) среди всех деревьев, не допускающих ошибок на обучении — в этом случае можно было бы надеяться на наличие у дерева обобщающей способности. К сожалению, эта задача является NP-полной, и поэтому приходится ограничиваться жадными алгоритмами построения дерева.

Опишем базовый жадный алгоритм построения бинарного решающего дерева. Начнем со всей обучающей выборки $$X$$ и найдем наилучшее ее разбиение на две части $$R_1(j, t) = \{ x| x_j < t \}$$, $$R_2(j,t) = \{ x|x_j \ge t \}$$ с точки зрения заранее заданного функционала качества $$Q(X, j, t)$$. Найдя наилучшие значения $$j$$ и $$t$$ , создадим корневую вершину дерева, поставив ей в соответствие предикат $$[x_j < t]$$ Объекты разобьются на две части — одни попадут в левое поддерево, другие в правое. Для каждой из этих подвыборок рекурсивно повторим процедуру, построив дочерние вершины для корневой, и так далее. В каждой вершине мы проверяем, не выполнилось ли некоторое условие останова — и если выполнилось, то прекращаем рекурсию и объявляем эту вершину листом. Когда дерево построено, каждому листу ставится в соответствие ответ. В случае с классификацией это может быть класс, к которому относится больше всего объектов в листе, или вектор вероятностей (скажем, вероятность класса может быть равна доле его объектов в листе). Для регрессии это может быть среднее значение, медиана или другая функция от целевых переменных объектов в листе. Выбор конкретной функции зависит от функционала качества в исходной задаче.

Решающие деревья могут обрабатывать пропущенные значения — ситуации, в которых для некоторых объектов неизвестны значения одного или нескольких признаков. Для этого необходимо модифицировать процедуру разбиения выборки в вершине, что можно сделать несколькими способами.

После того, как дерево построено, можно провести его _стрижку _(pruning) — удаление некоторых вершин с целью понижения сложности и повышения обобщающей способности. Существует несколько подходов к стрижке, о которых мы немного упомянем ниже.

Таким образом, конкретный метод построения решающего дерева определяется:

1. Видом предикатов в вершинах;
2. Функционалом качества $$Q(X, j,t)$$&#x20;
3. Критерием останова;
4. Методом обработки пропущенных значений;
5. Методом стрижки.

Также могут иметь место различные расширения, связанные с учетом весов объектов, работой с категориальными признакам и т.д. Ниже мы обсудим варианты каждого из перечисленных пунктов.

### Критерии информативности

При построении дерева необходимо задать функционал качества, на основе которого осуществляется разбиение выборки на каждом шаге. Обозначим через $$R_m$$ множество объектов, попавших в вершину, разбиваемую на данном шаге, а через $$R_l$$ и $$R_r$$ — объекты, попадающие в левое и правое поддерево соответственно при заданном предикате. Мы будем использовать функционалы следующего вида:

$$
Q(R_m, j, s) = H(R_m) - \frac{|R_l| }{|R_m|}H(R_l) - \frac{|R_r|}{|R_m|} H(R_r)
$$

Здесь $$H(R)$$ — это _критерий информативности_ (impurity criterion), который оценивает качество распределения целевой переменной среди объектов множества $$R$$. Чем меньше разнообразие целевой переменной, тем меньше должно быть значение критерия информативности — и, соответственно, мы будем пытаться минимизировать его значение. Функционал качества $$Q(R_m, j, s)$$ мы при этом будем максимизировать.

Как уже обсуждалось выше, в каждом листе дерево будет выдавать константу — вещественное число, вероятность или класс. Исходя из этого, можно предложить оценивать качество множества объектов $$R$$ тем, насколько хорошо их целевые переменные предсказываются константой (при оптимальном выборе этой константы):

$$
H(R) = \min\limits_{c \in \mathbb{Y}} \frac{1}{|R|} \sum_{(x_i, y_i) \in R} L(y_i, c)
$$

где$$L(y, c)$$ — некоторая функция потерь. Далее мы обсудим, какие именно критерии информативности часто используют в задачах регрессии и классификации.

### Регрессия

Как обычно, в регрессии выберем квадрат отклонения в качестве функции потерь. В этом случае критерий информативности будет выглядеть как

$$
H(R) = \min\limits_{c \in \mathbb{Y}} \frac{1}{|R|} \sum_{(x_i, y_i) \in R} (y_i - c)^2
$$

Как известно, минимум в этом выражении будет достигаться на среднем значении целевой переменной. Значит, критерий можно переписать в следующем виде:

$$
H(R) = \frac{1}{|R|} \sum_{(x_i, y_i) \in R} \bigg(
y_i - \frac{1}{|R|} \sum_{(x_j, y_j) \in R} y_j
 \bigg)^2
$$

Мы получили, что информативность вершины измеряется её дисперсией — чем ниже разброс целевой переменной, тем лучше вершина. Разумеется, можно использовать и другие функции ошибки $$L$$ — например, при выборе абсолютного отклонения мы получим в качестве критерия среднее абсолютное отклонение от медианы.

### Классификация

Обозначим через $$p_k$$ долю объектов класса $$k (k \in \{1, . . . , K\})$$ , попавших в вершину $$R$$:

$$
p_k =\frac{1}{|R|} \sum_{(x_i, y_i) \in R} [y_i = k]
$$

Через $$k_∗$$ обозначим класс, чьих представителей оказалось больше всего среди объектов, попавших в данную вершину: $$k_∗ = \arg \max\limits_kp_k$$ .

**Ошибка классификации**

Рассмотрим индикатор ошибки как функцию потерь:

$$
H(R) = \min\limits_{c \in \mathbb{Y}} \frac{1}{|R|} \sum_{(x_i, y_i) \in R} [y_i \ne c]
$$

Легко видеть, что оптимальным предсказанием тут будет наиболее популярный класс $$k_∗$$ — значит, критерий будет равен следующей доле ошибок:

$$
H(R) = \frac{1}{|R|} \sum_{(x_i, y_i) \in R} [y_i \ne k_* ] = 1 - p_{k_*}
$$

Данный критерий является достаточно грубым, поскольку учитывает частоту $$p_{k_∗}$$ лишь одного класса.

### Критерий Джинни для деревьев решений

Рассмотрим ситуацию, в которой мы выдаём в вершине не один класс, а распределение на всех классах $$c = (c_1, . . . , c_K), \sum_{k=1}^K c_k = 1$$. Качество такого распределения можно измерять, например, с помощью _критерия Бриера_ (Brier score):

$$
H(R) = \min\limits_{\sum_k c_k=1}\frac{1}{|R|}\sum_{(x_i, y_i) \in R} \sum_{k=1}^K (c_k - [y_i =k])^2
$$

Можно показать, что оптимальный вектор вероятностей состоит из долей классов $$p_k$$: $$c_* = (p_1, ..., p_k)$$&#x20;

Если подставить эти вероятности в исходный критерий информативности и провести ряд преобразований, то мы получим критерий Джини:

$$
H(R) = \sum_{k=1}^K p_k (1 - p_k)
$$

### Энтропийный критерий

Мы уже знакомы с более популярным способом оценивания качества вероятностей — логарифмическими потерями, или логарифмом правдоподобия:

$$
H(R) = \min\limits_{\sum_k c_k =1} \bigg( 
-\frac{1}{|R|} \sum_{(x_i, y_i) \in R} \sum_{k=1}^K [y_i = k] \log c_k
\bigg)
$$

Для вывода оптимальных значений $$c_k$$ вспомним, что все значения $$c_k$$ должны суммироваться в единицу. Подставляя эти выражения в критерий, получим, что он будет представлять собой энтропию распределения классов:

$$
H(R) = - \sum_{k=1}^K p_klog p_k
$$

Из теории вероятностей известно, что энтропия ограничена снизу нулем, причем минимум достигается на вырожденных распределениях $$(p_i = 1, p_j = 0 \text{ для } i \ne j)$$. Максимальное же значение энтропия принимает для равномерного распределения. Отсюда видно, что энтропийный критерий отдает предпочтение более «вырожденным» распределениям классов в вершине.

### Критерий останова

Можно придумать большое количестве критериев останова. Перечислим некоторые ограничения и критерии:

* Ограничение максимальной глубины дерева.
* Ограничение минимального числа объектов в листе.
* Ограничение максимального количества листьев в дереве.
* Останов в случае, если все объекты в листе относятся к одному классу.
* Требование, что функционал качества при дроблении улучшался как минимум на $$s$$ процентов.

С помощью грамотного выбора подобных критериев и их параметров можно существенно повлиять на качество дерева. Тем не менее, такой подбор является трудозатратным и требует проведения кросс-валидации.

### Методы стрижки дерева

Стрижка дерева является альтернативой критериям останова, описанным выше. При использовании стрижки сначала строится переобученное дерево (например, до тех пор, пока в каждом листе не окажется по одному объекту), а затем производится оптимизация его структуры с целью улучшения обобщающей способности. Существует ряд исследований, показывающих, что стрижка позволяет достичь лучшего качества по сравнению с ранним остановом построения дерева на основе различных критериев.

Тем не менее, на данный момент методы стрижки редко используются и не реализованы в большинстве библиотек для анализа данных. Причина заключается в том, что деревья сами по себе являются слабыми алгоритмами и не представляют большого интереса, а при использовании в композициях они либо _должны _быть переобучены (в случайных лесах), либо должны иметь очень небольшую глубину (в бустинге), из-за чего необходимость в стрижке отпадает.

Одним из методов стрижки является _cost-complexity pruning_. Обозначим дерево, полученное в результате работы жадного алгоритма, через $$T_0$$ . Поскольку в каждом из листьев находятся объекты только одного класса, значение функционала $$R(T)$$ будет минимально на самом дереве $$T_0$$ (среди всех поддеревьев).

Однако данный функционал характеризует лишь качество дерева на обучающей выборке, и чрезмерная подгонка под нее может привести к переобучению. Чтобы преодолеть эту проблему, введем новый функционал $$R_{\alpha}(T)$$ , представляющий собой сумму исходного функционала $$R(T)$$ и штрафа за размер дерева:

$$
R_{\alpha} (T) = R(T) + \alpha |T|
$$

где $$|T|$$ — число листьев в поддереве $$T$$ , а $$\alpha > 0$$ — параметр. Это один из примеров _регуляризованных _критериев качества, которые ищут баланс между качеством классификации обучающей выборки и сложностью построенной модели.

Можно показать, что существует последовательность вложенных деревьев с одинаковыми корнями:

$$
T_k \subset T_{K-1} \subset ... \subset T_0
$$

здесь $$T_K$$ — тривиальное дерево, состоящее из корня дерева $$T_0$$, в которой каждое дерево $$T_i$$ минимизирует критерий для $$\alpha$$ из интервала $$α ∈ [α_i , α_i+1)$$ , причем

$$
0 = \alpha_0 < \alpha_1< ... < \alpha_K < \infty
$$

Эту последовательность можно достаточно эффективно найти путем обхода дерева. Далее из нее выбирается оптимальное дерево по отложенной выборке или с помощью кросс-валидации.

### Учет категориальных признаков

Самый очевидный способ обработки категориальных признаков — разбивать вершину на столько поддеревьев, сколько имеется возможных значений у признака (multi-way splits). Такой подход может показывать хорошие результаты, но при этом есть риск получения дерева с крайне большим числом листьев.

Рассмотрим подробнее другой подход. Пусть категориальный признак xj имеет множество значений $$Q = \{u_1, . . . , u_q\}, |Q| = q$$. Разобьем множество значений на два непересекающихся подмножества: $$Q = Q_1 \sqcup Q_2$$, и определим предикат как индикатор попадания в первое подмножество: $$\beta (x) = [x_j \in Q_1]$$. Таким образом, объект будет попадать в левое поддерево, если признак $$x_j$$ попадает в множество $$Q_1$$и в первое поддерево в противном случае. Основная проблема заключается в том, что для построения оптимального предиката нужно перебрать $$2^{q -1} - 1$$ вариантов разбиения, что может быть не вполне возможным. Оказывается, можно обойтись без полного перебора в случаях с бинарной классификацией и регрессией. Обозначим через $$R_m(u)$$множество объектов, которые попали в вершину $$m$$ и у которых $$j$$ -й признак имеет значение $$u$$, через $$N_m(u)$$ обозначим количество таких объектов.&#x20;

В случае с бинарной классификацией упорядочим все значения категориального признака на основе того, какая доля объектов с таким значением имеет класс +1:

$$
\frac{1}{N_m(u_{(1)})} \sum_{x_i \in R_m(u_{(1)})}  [y_i = +1] \le .. \le \frac{1}{N_m(u_{(q)})} \sum_{x_i \in R_m(u_{(q)})} [y_i = +1]
$$

после чего заменим категорию $$u_{(i)}$$ на число $$i$$ , и будем искать разбиение как для вещественного признака.
