---
description: 'Цель работы: ознакомится с основами нечеткого вывода'
---

# Практическая 5. Нечеткий вывод

## Теоретические сведения

Программный пакет fuzzyTECH разработан и постоянно модифицируется немецкой компанией Infoi'm GmbH \(Inform Software Corporation\). Он предназначен для решения различных задач нечеткого моделирования и управления объектами в условиях трудно оцениваемых и контролируемых возмущений.

По сравнению с пакетом Fuzzy Logic Toolbox, входящим в Matlab, пакет fuzzyTECH является специализированным средством, которое позволяет разрабатывать разнообразные нечеткие системы в графическом режиме, а также транслировать их в программу на одном из языков программирования, в том числе и для реализации ее в программируемых микроконтроллерах.

Для обеспечения возможности создания, отладки и оптимизации разрабатываемых нечетких систем, в состав пакета fuzzyTECH v5.xx включены следующие основные элементы:

* средство просмотра параметров рабочего проекта в виде дерева \(TreeView\);
* редактор проекта \(Project Editor\);
* отладчик \(Debugger\);
* анализатор \(Analyzer\);
* генератор кода \(Code Generator\). 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 1 - &#x41E;&#x441;&#x43D;&#x43E;&#x432;&#x43D;&#x43E;&#x435; &#x43E;&#x43A;&#x43D;&#x43E; &#x43F;&#x440;&#x43E;&#x433;&#x440;&#x430;&#x43C;&#x43C;&#x44B; fuzzyTECH](../.gitbook/assets/image%20%2833%29.png)

### Редактор проекта \(Project Editor\)

Еще одним важным элементом пакета fuzzyTECH, который предназначен для графического отображения структуру редактируемого проекта, является редактор проекта \(Project Editor\). Окно редактора создается при запуске fuzzyTECH и не может быть закрыто в течение всей работы с программой. Единственной возможностью скрыть окно редактора проекта является его минимизация \(функция «свернуть в значок» системного меню главного окна программы\).

Редактор использует три основных вида ресурсов: _текст, переменные, базы правил_. 

**Текст**. Данный ресурс используется для придания большей наглядности разрабатываемому проекту. Текст может быть помещен в любое место на рабочем листе, возможно написание его различными шрифтами, стилями, цветом. 

**Переменные**. Каждая переменная входа/выхода разрабатываемой нечеткой логической модели связана со своим отображением - интерфейсом на рабочем листе редактора проектов \(Example variable \(a\) на рис.2\). Интерфейс переменной представляет собой небольшой прямоугольник, в котором отображаются имя переменной и иконка. В случае выходных переменных иконка отображает способ их вычисления \(SoM, MoM и т.д.\). При этом для входных переменных иконка расположена ближе к левому краю прямоугольника, а для выходной переменной – ближе к правому краю. Вспомогательные переменные, используемые в проекте, не связываются ни с каким интерфейсом и действуют только внутри блока правил, к которому они относятся. 

**Блок правил**. В пакете fuzzyTECH принята идеология, когда индивидуальные правила вывода объединяются в блоки \(Rule Block \(b\) на рис. 2\) для более наглядного представления структуры проекта. При этом в одном проекте может быть несколько таких блоков. Блок правил \(Rule Block\) состоит из колонок переменных и двух прямоугольников-операторов. В левой колонке отображаются переменные, используемые в качестве условий нечетких правил \(часть правила «ЕСЛИ»\), а в правой колонке – переменные, получаемые в ходе применений правил логического вывода \(часть правил «ТО»\). 

В свою очередь, верхний прямоугольник блока правил содержит информацию об операторе, применяемом для объединения входных условий \(оператор «MIN»\), а в нижнем прямоугольнике – информация об операторе, используемом для объединения результатов расчета модели \(оператор «MAX»\). Информационные потоки между лингвистическими переменными отображаются с помощью линий, связанными с различными ресурсами проекта.

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 2 - &#x41F;&#x440;&#x438;&#x43C;&#x435;&#x440; &#x432;&#x441;&#x435;&#x445; &#x442;&#x438;&#x43F;&#x43E;&#x432; &#x43E;&#x43F;&#x435;&#x440;&#x430;&#x442;&#x43E;&#x440;&#x43E;&#x432; &#x432; &#x43F;&#x440;&#x43E;&#x435;&#x43A;&#x442;&#x435; fuzzyTECH](../.gitbook/assets/image%20%2832%29.png)

### Создание и работа с переменными

Для создания переменной можно использовать дерево проекта \(Treeview\) или воспользоваться иконкой создания новой переменной ![](../.gitbook/assets/image%20%2835%29.png) .

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 3 - &#x421;&#x43E;&#x437;&#x434;&#x430;&#x43D;&#x438;&#x435; &#x43D;&#x43E;&#x432;&#x43E;&#x439; &#x43F;&#x435;&#x440;&#x435;&#x43C;&#x435;&#x43D;&#x43D;&#x43E;&#x439; &#x438;&#x437; Treeview](../.gitbook/assets/image%20%2838%29.png)

После выбора пункта создания новой переменной, открывается окно представленное на рисунке 4. В окне можно настроить параметры переменной: имя \(Name\), метод вычисления значения переменной относительно ее лингвистических термов \(method\), комментарий относительно содержания переменной \(comment\), лингвистические термы связанные с переменной \(Terms\). В нижней части окна расположена другая таблица предназначенная для настройки диапазона переменной \(в демо версии fuzzyTECH доступен только тип double\). Параметр shell value minimum отвечает за нижнюю границу переменной, shell value maximum за верхнюю границу переменной, shell value default за значение хранящееся в переменной по-умолчанию. 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 4 - &#x41E;&#x43A;&#x43D;&#x43E; &#x43F;&#x430;&#x440;&#x430;&#x43C;&#x435;&#x442;&#x440;&#x43E;&#x432; &#x43F;&#x435;&#x440;&#x435;&#x43C;&#x435;&#x43D;&#x43D;&#x43E;&#x439;](../.gitbook/assets/image%20%2825%29.png)

После настройки параметров переменной можно перейти к настройке функции принадлежности термов переменной. Для этого можно воспользоваться контекстным меню, пункт Edit variable. В окне редактора \(рис 5.\) можно настроить параметры функций принадлежности лингвистических термов. 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 5 - &#x41E;&#x43A;&#x43D;&#x43E; &#x440;&#x435;&#x434;&#x430;&#x43A;&#x442;&#x43E;&#x440;&#x430; &#x43F;&#x435;&#x440;&#x435;&#x43C;&#x435;&#x43D;&#x43D;&#x43E;&#x439;](../.gitbook/assets/image%20%2834%29.png)

Выбрав одну из функций принадлежности терма можно подробно ее настроить, как в окне графиков, так и в окне параметров функции принадлежности \(рис. 6\). 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 6 - &#x413;&#x440;&#x430;&#x444;&#x438;&#x447;&#x435;&#x441;&#x43A;&#x438;&#x439; &#x43C;&#x435;&#x442;&#x43E;&#x434; &#x440;&#x430;&#x431;&#x43E;&#x442;&#x44B; &#x441; &#x444;&#x443;&#x43D;&#x43A;&#x446;&#x438;&#x44F;&#x43C;&#x438; &#x43F;&#x440;&#x438;&#x43D;&#x430;&#x434;&#x43B;&#x435;&#x436;&#x43D;&#x43E;&#x441;&#x442;&#x438;](../.gitbook/assets/fabrika-formatov-zapis-s-ekrana20200817_104953.gif)

При помощи контекстного меню терма возможна подробная настройка функции принадлежности \(рис. 7\). 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 7 - &#x41A;&#x43E;&#x43D;&#x442;&#x435;&#x43A;&#x441;&#x442;&#x43D;&#x43E;&#x439; &#x43C;&#x435;&#x43D;&#x44E; &#x442;&#x435;&#x440;&#x43C;&#x430; &#x432; &#x43E;&#x43A;&#x43D;&#x435; &#x440;&#x435;&#x434;&#x430;&#x43A;&#x442;&#x43E;&#x440;&#x430;](../.gitbook/assets/image%20%2823%29.png)

После выбора пункта редактирования терма открывается окно редактора \(рис. 8\).  В окне редактора можно выбрать тип функции принадлежности \(type\). Доступны 4 основные функции принадлежности, булевы операции. В строке membership function можно установить точки интервала, к которым будет привязана функция. При двойном щелчке на строку открывается окно редактора функции принадлежности \(рис. 9\). 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 8 - &#x41E;&#x43A;&#x43D;&#x43E; &#x440;&#x435;&#x434;&#x430;&#x43A;&#x442;&#x43E;&#x440;&#x430; &#x442;&#x435;&#x440;&#x43C;&#x430;](../.gitbook/assets/image%20%2826%29.png)

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 9 - &#x41E;&#x43A;&#x43D;&#x43E; &#x440;&#x435;&#x434;&#x430;&#x43A;&#x442;&#x43E;&#x440;&#x430; &#x444;&#x443;&#x43D;&#x43A;&#x446;&#x438;&#x438; &#x43F;&#x440;&#x438;&#x43D;&#x430;&#x434;&#x43B;&#x435;&#x436;&#x43D;&#x43E;&#x441;&#x442;&#x438;](../.gitbook/assets/image%20%2836%29.png)

В окне редактора два столбца: значение точки параметра \( $$x$$ \) и значение функции принадлежности в этой точке \($$\mu$$\). Функция принадлежности \(линейная\) обладает свойством непрерывности, поэтому первая и последняя точка функции создаются автоматически. Для того что бы создать новую точку можно воспользоваться иконкой ![](../.gitbook/assets/image%20%2840%29.png). В левом столбце назначается точка на оси параметра, а в правом значение функции принадлежности \(от 0 до 100\). 



### Создание и работа с блоками правил 

Создать блок правил можно как из  дерева проектов, так и при помощи иконки ![](../.gitbook/assets/image%20%2831%29.png) в меню. После создания блока необходимо назначить входные и выходные переменные, при помощи контекстного меню \(рисунок 10\). 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 10 - &#x41D;&#x430;&#x437;&#x43D;&#x430;&#x447;&#x435;&#x43D;&#x438;&#x435; &#x432;&#x445;&#x43E;&#x434;&#x43D;&#x43E;&#x439; &#x43F;&#x435;&#x440;&#x435;&#x43C;&#x435;&#x43D;&#x43D;&#x43E;&#x439;](../.gitbook/assets/image%20%2829%29.png)

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 11 - &#x411;&#x43B;&#x43E;&#x43A; &#x43F;&#x440;&#x430;&#x432;&#x438;&#x43B; &#x441; &#x43D;&#x430;&#x437;&#x43D;&#x430;&#x447;&#x435;&#x43D;&#x43D;&#x43E;&#x439; &#x432;&#x445;&#x43E;&#x434;&#x43D;&#x43E;&#x439; &#x438; &#x432;&#x44B;&#x445;&#x43E;&#x434;&#x43D;&#x43E;&#x439; &#x43F;&#x435;&#x440;&#x435;&#x43C;&#x435;&#x43D;&#x43D;&#x43D;&#x43E;&#x439;](../.gitbook/assets/image%20%2820%29.png)

После назначения переменных необходимо задать правила вывода. Для перехода к параметрам блока можно воспользоваться контекстным меню \(правая кнопка мыши\) \(рис. 12\).

 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 12 - &#x41A;&#x43E;&#x43D;&#x442;&#x435;&#x43A;&#x441;&#x442;&#x43D;&#x43E;&#x435; &#x43C;&#x435;&#x43D;&#x44E; &#x431;&#x43B;&#x43E;&#x43A;&#x430; &#x43F;&#x440;&#x430;&#x432;&#x438;&#x43B;](../.gitbook/assets/image%20%2822%29.png)

После выбора редактора открывается окно параметров блока правил \(рис.13\). 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 13 - &#x41E;&#x43A;&#x43D;&#x43E; &#x440;&#x435;&#x434;&#x430;&#x43A;&#x442;&#x43E;&#x440;&#x430; &#x43F;&#x440;&#x430;&#x432;&#x438;&#x43B;](../.gitbook/assets/image%20%2821%29.png)

По-умолчанию, для одной входной переменной и одной выходной переменной назначается минимаксное правило вывода. Для рассмотрения механизма создания правил добавим дополнительную переменную в модель. После назначения дополнительной входной переменной внешний вид редактора блока правил изменяется \(рис. 14\). 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 14 - &#x420;&#x435;&#x434;&#x430;&#x43A;&#x442;&#x43E;&#x440; &#x43F;&#x440;&#x430;&#x432;&#x438;&#x43B; &#x43F;&#x43E;&#x441;&#x43B;&#x435; &#x434;&#x43E;&#x431;&#x430;&#x432;&#x43B;&#x435;&#x43D;&#x438;&#x44F; &#x43F;&#x435;&#x440;&#x435;&#x43C;&#x435;&#x43D;&#x43D;&#x43E;&#x439;](../.gitbook/assets/image%20%2837%29.png)

Для создания нового ряда правил можно воспользоваться иконкой ![](../.gitbook/assets/image%20%2828%29.png). После создания нового ряда можно начать составление правила. Для переменных правила назначаются условные значения, определенные в термах переменной \(рис. 15\). 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 15 - &#x412;&#x44B;&#x431;&#x43E;&#x440; &#x442;&#x435;&#x440;&#x43C;&#x430; &#x43F;&#x435;&#x440;&#x435;&#x43C;&#x435;&#x43D;&#x43D;&#x43E;&#x439; &#x432; &#x43F;&#x440;&#x430;&#x432;&#x438;&#x43B;&#x435; ](../.gitbook/assets/image%20%2839%29.png)

После настройки переменных правила, можно настроить параметр значения вывода \(рис. 16\). В примере дополнительной колонкой является процент уверенности в выводе правила. 

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 16 - &#x41F;&#x440;&#x438;&#x43C;&#x435;&#x440; &#x43F;&#x440;&#x430;&#x432;&#x438;&#x43B;&#x430; &#x432; &#x431;&#x43B;&#x43E;&#x43A;&#x435; &#x43F;&#x440;&#x430;&#x432;&#x438;&#x43B;](../.gitbook/assets/image%20%2841%29.png)

На языке описания правил сконфигурированное правило можно описать так: 

```text
ЕСЛИ (example = low) И (example2 = low) ТОГДА (output_example = low (100%)) 
```

### Отладка модели нечеткого вывода

Для проверки работы модели можно воспользоваться визуальным отладчиком. Вызвать его можно нажав на иконку ![](../.gitbook/assets/image%20%2824%29.png), в строке меню или воспользовавшись вкладкой **Debug -&gt; Interactive.** 

Отладчик представлен на рисунке 17. В списке в левой части окна представлены входные переменные, в списке в правой части окна представлены выходные переменные модели. При помощи пункта ввода или ползунка можно назначить значение входной переменной и увидеть значение выходной в скобках в правой части окна.

![&#x420;&#x438;&#x441;&#x443;&#x43D;&#x43E;&#x43A; 17 - &#x41E;&#x43A;&#x43D;&#x43E; &#x43E;&#x442;&#x43B;&#x430;&#x434;&#x43A;&#x438;](../.gitbook/assets/image%20%2827%29.png)

##  Ход работы

### Задание 1. 

Составить модель нечеткого вывода для следующих задач: 

1. Задача о выборе томатов. По производственной линии транспортируют томаты, их необходимо разделить на три категории: Премиум, Обычные, Эконом. Во время транспортировки томаты взвешивают и измеряют их диаметр. Необходимо определить степень спелости томата и отнести его к одной из категорий.  
2. Задача о выпуске парашюта. Для успешного возвращения ракеты, необходим блок спасения, выпускающий парашют при совокупности событий: нужная высота, нужные координаты. Необходимо составить правила управления блоком спасения. 
3. Задача о правильном количестве специй. При приготовлении блюда важно соблюдать баланс специй для правильного ощущения вкуса. Известный повар обратился к вам с просьбой составить правила для устройства которое в зависимостимости от количества добавленных специй \(соль, сахар, перец\) сможет предсказать насколько вкусным будет блюдо. Повара используют следующую шкалу для оценивания количества специй: Чуть-чуть, Горсточка, Горсть, Много. Для оценки вкуса используется следующая шкала: Пресно, Сьедобно, Хорошо, Несьедобно. 

### Критерии оценки практического занятия

Оценивается знание материала, способность к его обобщению, критическому осмыслению, систематизации. 

* 3 балла: студент полностью выполнил задания.
* 2 балла: в усвоении учебного материала допущены небольшие пробелы.
* 1 балл: неполно или непоследовательно реализовано задание.
* 0 баллов: не раскрыто основное содержание учебного материала.

**Максимальный балл: 3 балла**

