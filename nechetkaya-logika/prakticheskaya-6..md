---
description: 'Цель работы: ознакомится с механизмом работы и созданием нечетких контроллеров'
---

# Практическая 6. Нечеткий контроллер

## Теоретические сведения

### Нечеткие управляющие системы

В работе сформулированы пять принципов организации интеллектуальной управляющей структуры. 

_Первый принцип._ Наличие взаимодействия управляющих систем с реальным внешним миром с использованием информационных каналов связи. 

_Второй принцип._ Принципиальная открытость систем с целью повышения интеллектуальности и совершенствования собственного поведения.

_Третий принцип._ Наличие механизмов прогноза изменений внешнего мира и собственного поведения системы в динамически меняющемся внешнем мире. 

_Четвёртый принцип._ Наличие у управляющей системы многоуровневой иерархической структуры, построенной в соответствии с правилом повышения интеллектуальности и снижения требований к точности моделей по мере повышения ранга иерархии в системе \(и наоборот\). 

_Пятый принцип._ Сохраняемость функционирования \(возможно, с некоторой потерей качества или эффективности, иначе с некоторой деградацией\) при разрыве связей или потере управляющих воздействий от высших уровней иерархии управляющей структуры.

В соответствии с этими принципами были определены два типа интеллектуальных управляющих систем. 

_Определение 1._ Управляющие системы, организованные и функционирующие в соответствии со сформулированными пятью принципами \(в полном их объёме\), называются управляющими системами, обладающими свойством "интеллектуальности в большом". 

_Определение 2._ Управляющие системы, структурно не организованные в соответствии с приведёнными выше пятью принципами, но использующие при функционировании знания \(например в виде правил\) как средство преодоления неопределённости входной информации, модели управляемого объекта или его поведения, называются управляющими системами, обладающими свойством "интеллектуальности в малом". Примером управляющих систем со свойством "интеллектуальности в малом" служат нечёткие контроллеры. 

_Определение 3_. Нечётким регулятором \(контроллером\) называется иерархическая двухуровневая система управления, "интеллектуальная в малом", на нижнем \(исполнительном\) уровне которой находится традиционный ПИД-регулятор, а на верхнем координационном уровне используется база знаний \(с блоком нечёткого вывода в виде продукционных правил с нечёткой импликацией\) и устройства перевода в лингвистические и в чёткие значения \(фазификатор и дефазификатор соответственно\).

Как правило, во всех нечётких регуляторах используется основной принцип регулирования – принцип регулирования по отклонению. Выходная переменная объекта управления сравнивается с заданным значением $$x_r$$, ошибка рассогласования

$$
E = x_r - x
$$

обычно подвергается различным масштабным преобразованиям. Кроме самого значения рассогласования вычисляется скорость изменения рассогласования $$E^*$$ . Полученные числовые значения преобразуются фазификатором в соответствующие лингвистические значения.

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 1 - &#x410;&#x440;&#x445;&#x438;&#x442;&#x435;&#x43A;&#x442;&#x443;&#x440;&#x430; &#x43D;&#x435;&#x447;&#x435;&#x442;&#x43A;&#x43E;&#x433;&#x43E; &#x43A;&#x43E;&#x43D;&#x442;&#x440;&#x43E;&#x43B;&#x43B;&#x435;&#x440;&#x430;](../.gitbook/assets/image%20%2844%29.png)

Для построения базы знаний нечёткого контроллера может использоваться и более сложная структура: "ситуация – стратегия управления – действие". Кроме рассмотренной структуры возможны и более сложные, способные адаптировать к изменениям окружающей среды путем переключений на другие множества лингвистических значений, продукционные правила, базы знаний.

Совокупность – фазификатор, процесс вывода, дефазификатор – можно рассматривать как нечёткий процессор \(НПР\). В реализации последнего в настоящее время возможны следующие направления:

1. программная эмуляция нечётких процессоров на персональных компьютерах или промышленных контроллерах;
2. применение плат-ускорителей для ПК, реализующих нечёткие алгоритмы управления; 
3. создание специализированных нечётких процессоров. 

Эмуляция нечётких процессоров на персональных компьютерах не вызывает в настоящее время каких-либо затруднений. Аппаратные и программные возможности современных ПК позволяют воспроизводить все необходимые операции. 

Однако требование управления в реальном масштабе времени может быть обеспечено традиционными ПК на ограниченном количестве продукционных правил. Значительно лучшие перспективы здесь имеют ЭВМ на RISC-процессорах. Общим недостатком этих решений является аппаратная и программная избыточность подобных решений.

### Принципы адаптации в нечетком управлении

Сама идея нечеткого управления, воспроизводящая в определенной степени методы интеллектуального управления, может быть в неявном виде, предполагает возможность адаптации. 

Уровень реализации этой возможности зависит и от сложности решения задач и от ресурсов, которые можно использовать. 

Первый, наиболее простой вариант адаптации заключается в том, что в нечетком контроллере более конкретно в базе знаний, предусмотрен счетчик интенсивности использования правил нечеткого вывода. После некоторого количества циклов управления возможны перегруппировка правил в базе знаний, создание своего рода кэш-памяти, когда наиболее интенсивно используемые правила размещаются в области с меньшим временем доступа. Правила, интенсивность использования которых минимальна, наоборот, помещаются в область с большим временем доступа. Возможно также и удаление правил из базы знаний. 

Второй вариант адаптации заключается в том, что в случае возникновения ситуации, для которой отсутствует напрямую связанное с ней правило нечеткого вывода, система делает попытку либо найти ближайшее правило или комбинацию правил и на их основе выполнить вывод, либо сформулировать новое правило, ранее отсутствующее в системе. Одним из вариантов решения этой задачи может быть следующий. Пусть ситуация по переменным, характеризующим систему в некоторый момент времени, определяется нечеткими множествами

$$
\tilde{A} = \{ \mu_a (x) / x \}, \tilde{B} = \{ \mu_b (y) / y \}, W = \{ \mu_w(z) / z \}
$$

В базе знаний системы нет правила, в условной части которого находится этот набор полностью. Однако находятся правила, содержащие отдельные фрагменты этого набора. Естественным выбором является то правило, которое содержит фрагмент, наиболее близкий к рассматриваемой комбинации. Степень близости можно, например, оценить по величине взвешенной мощности свертки нечетких множеств. Возможен и другой подход. В системе нечеткого управления для переменной, определяющей управляющее воздействие, определено множество ее лингвистических значений $$L_y$$ и соответствующие нечеткие множества:

$$
L_y = \{ \mu_{L1} (\xi) / \xi \, \mu_{L2}(\xi)/ \xi, ...\}
$$

Для неизвестного набора вычисляется свертка соответствующих нечетких множеств и определяется импликация:

$$
\tilde{S} \to L_i, i = 1, 2, ...
$$

где $$\tilde{S}$$ – cвертка нечетких множеств, входящих в неизвестный набор. Импликация, в свою очередь, является нечетким множеством, и в качестве наиболее соответствующей данной ситуации выбирается та, для которой максимально значение взвешенной мощности. К недостаткам рассмотренных методов следует отнести то, что их реализация занимает большое время, т.е. не может быть обеспечена в реальном масштабе времени. В ряде случаев, например при управлении электроприводом, может быть использована адаптация с эталонной моделью \(рис. 2\).

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 2 - &#x410;&#x440;&#x445;&#x438;&#x442;&#x435;&#x43A;&#x442;&#x443;&#x440;&#x430; &#x443;&#x43F;&#x440;&#x430;&#x432;&#x43B;&#x435;&#x43D;&#x438;&#x44F; &#x441; &#x44D;&#x442;&#x430;&#x43B;&#x43E;&#x43D;&#x43D;&#x43E;&#x439; &#x43C;&#x43E;&#x434;&#x435;&#x43B;&#x44C;&#x44E;](../.gitbook/assets/image%20%2842%29.png)

$$U = g + z$$– управляющее содействие; 

$$X_1, X_2$$ – выходные координаты объекта управления; 

$$g$$ – задающее воздействие; 

$$Z$$ – выходная скалярная переменная нечеткого контроллера;

$$X_{1m}, X_{2m}$$ – выходные координаты эталонной модели; 

$$e_1 = X_1 - X_{1m} , e_2 = X_2 -X_{2m}$$ сигналы ошибки;

$$E_1, E_2$$ – выходные координаты фазификатора. 

Нечеткий контроллер вырабатывает сигнал адаптации в зависимости от величины расхождения между выходными координатами объекта управления и эталонной модели. 

В зависимости от особенностей объекта управления могут использоваться эталонная модель традиционного типа либо нечеткая модель. 

Адаптация нечеткого контроллера может заключаться в изменении правых частей тех правил базы правил, которые приводят к низкому качеству управления.

Общая идея адаптивных систем заключается во введении в систему управления дополнительного контура адаптации, который обеспечивает коррекцию закона управления. 

Адаптация с коррекцией правил заключается в следующем. Адаптивный нечеткий регулятор \(рис. 3\) оценивает информацию об изменении параметров объекта управления по значениям ошибки управления и ее производной $$\partial E / \partial t$$. Контур адаптации формирует корректирующее воздействие, изменяя правые части правил нечеткого управления. Таблица лингвистических правил \(ТЛП\) адаптации использует информацию о желаемом отклике системы в виде таблицы соответствий. Некоторые ситуации $$(E, \partial E / \partial t)$$воспринимаются как соответствующие нормальному протеканию переходного процесса, другие воспринимаются как требующие коррекции. Коррекция правил заключается в изменении не текущего правила, а предыдущего правила, которое и создало неудовлетворительную текущую ситуацию.

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 3 - &#x410;&#x440;&#x445;&#x438;&#x442;&#x435;&#x43A;&#x442;&#x443;&#x440;&#x430; &#x441;&#x438;&#x441;&#x442;&#x435;&#x43C;&#x44B; &#x443;&#x43F;&#x440;&#x430;&#x432;&#x43B;&#x435;&#x43D;&#x438;&#x44F; &#x441; &#x43A;&#x43E;&#x440;&#x440;&#x435;&#x43A;&#x446;&#x438;&#x435;&#x439; ](../.gitbook/assets/image%20%2843%29.png)

Адаптация с выбором баз знаний предполагает использование различных наборов правил нечеткого управления для различных ситуаций. Отдельная база правил задает трехмерную $$(E^*, \partial{E}^*/ \partial{t}, U^*_c)$$ _поверхность управления._ 

Меняя параметры управления управляемого объекта и обучая каждый раз нечеткий регулятор, можно построить несколько таких поверхностей, которые могут быть близки между собой или сильно отличаться. Пересечения различных поверхностей могут соответствовать инвариантным правилам управления. При выполнении гипотезы о квазистационарности объекта управления \(обычной при постановке задач адаптивного управления\) нужно осуществить выбор между некоторым количеством баз знаний, соответствующих существенно различным параметрам объекта. Практически в такой системе используется несколько нечетких регуляторов со своими базами знаний, которые адаптированы для существенно различных параметров объектов. В процессе управления заранее неизвестно, какая база знаний является наиболее подходящей, поэтому входная ситуация $$(E, \partial{E}^*/ \partial{t})$$подается одновременно на все нечеткие регуляторы. Затем формируется интегральный управляющий сигнал, при этом предусматривается необходимость подавления сигнала с нечеткого регулятора, база знаний которого не соответствует текущим параметрам объекта. 

### Методы описания знаний в нечетких системах

Читатели, вероятно обратили внимание на то, что понятие качественный и нечеткий отнюдь не являются синонимами. Знания могут характеризоваться количественными и качественными показателями, быть четкими, имеющими математическое описание, и нечеткими, представленными лингвистическим конструкциями естественного языка, и эти пары признаков являются независимыми. 

Знание, оцениваемое качественно, т.е. не описанное цифрами и формулами, отнюдь не всегда является нечетким. Например: «это моя ручка» – четкое качественное знание; «это, похоже, моя ручка» – нечеткое качественное знание. Поэтому все базовые языки представления знаний могут описывать как знания четкие \(что и было проиллюстрировано приведенными выше примерами\), так и знания нечеткие. Следует обратить внимание еще и на то, что теперь речь идет не о новых базовых языках описания знаний, в данном случае знаний нечетких, а о способах описания нечеткости знаний, которые можно ввести в любом из описанных выше базовых языков. Например, может иметь место язык четких и нечетких продукционных правил, четких и нечетких семантических сетей и т.д. Итак, каким же образом трактуется понятие нечеткость и какие способы описания нечеткости знаний могут быть? 

К наиболее употребительным методам описания нечётких знаний относятся: методы теории многозначной логики, теории вероятностей, теории ошибок \(интервальные модели\), теории интервальных средних, теории субъективных вероятностей, теории нечетких множеств, теории нечетких мер и интегралов.

Следует отметить, что тот или иной способ описания нечеткости в разной степени совместим с тем или иным базовым языком представления знаний с точки зрения сложности описания и полноты возможностей получаемой формальной модели. А поскольку представление знаний является средством описания знаний человека, желательно, чтобы описательные возможности выбранного языка в конкретной предметной области были как можно выше. 

С этой точки зрения решение о форме представления знаний, принимаемое на одном из первых этапов проектирования, в значительной степени влияет на эффективность разрабатываемой интеллектуальной технической системы. Зачастую, возможностей одного даже самого подходящего языка оказывается недостаточно. Поэтому некоторые интеллектуальные системы имеют комплексное представление знаний, основанное на нескольких базовых языках представления знаний. С другой стороны, если форма представления знаний чрезмерно усложняется, то затрудняется техническая реализация такой интеллектуальной системы и возникает опасность потери достоверности выполняемых ею действий. В конечном итоге, выбор метода представления знаний представляет собой некий компромисс между универсальностью системы и возможностью ее технической реализации, с учетом конкретных прикладных задач, составляющих специализацию будущей интеллектуальной технической системы.

 Интеллектуальная САУ должна обладать, в определённой степени, такими возможностями человека, как способностью к обучению, адаптации, накоплению и систематизации знаний об объекте управления. Кроме того, изначально при создании интеллектуальной САУ система практически всегда содержит базовый набор знаний, полученных от специалистов в данной предметной области – экспертов и представленных в соответствии с выбранным языком представления знаний и методом описания их нечеткости. 

Так как знания и опыт человека имеют, в основном, вербальный характер, и едва ли не все рассуждения человека по своей природе являются приближенными, то наиболее перспективными являются интеллектуальные САУ, использующие для представления знаний человека о свойствах и принципах управления объектом лингвистические переменные и аппарат нечетких множеств. 

Целесообразность и перспективность именно этого подхода к описанию и представлению нечетких знаний в интеллектуальных САУ обоснованна тем, что вышеупомянутый математический аппарат оперирует с лексическими категориями оценок, восприятия и способов рассуждения человека, т.е. с нечеткими лингвистическими категориями, а согласно аксиоматике управления сложными слабоструктурированными объектами всю информацию об объекте управления и способах управления им можно выразить средствами обычного естественного языка. Кроме того, такой подход к представлению нечетких знаний существенно облегчает первоначальное «обучение» создаваемой интеллектуально системы группой экспертов, так как аппарат нечетких множеств, оперирующий лингвистическими переменными, позволяет наиболее точно реализовать машинную интерпретацию знаний экспертов. 

Это является немаловажным фактором при выборе методов представления нечетких знаний в интеллектуальных САУ, поскольку эксперты – это люди, которые обладают эмпирическими знаниями по управлению сложным объектом и, как и свойственно людям, оперируют лексическими категориями естественного языка при описании сложных объектов и правил управления этими объектами.

Поэтому, несмотря на то, что каждый из упомянутых выше четырёх наиболее общеупотребительных способов описания нечетких знаний заслуживает отдельного подробного описания \(чего невозможно сделать в пределах данного учебного пособия\), целесообразно рассматривать принципы и методы построения интеллектуальных САУ, основанных на представлении знаний методами теории нечетких множеств. Разумеется, не все проектируемые в настоящее время интеллектуальные САУ базируются на методах теории нечетких множеств при представлении знаний. Однако, как показывает анализ тенденций развития интеллектуальных оперирующих знаниями САУ, большинство интеллектуальных систем автоматизации, использующихся в промышленности при управлении слабоструктурированными объектами, базируются на нечетком представлении знаний методами теории нечетких множеств

## Контрольные вопросы

1. Как организуется база знаний в нечеткой системе управления доменной печью?
2. Что характеризует обобщенная функция принадлежности?
3. Чем можно объяснить перспективность нечетких систем управления в автомобилях?
4. Какие основные варианты адаптации используются в нечетких системах управления?


