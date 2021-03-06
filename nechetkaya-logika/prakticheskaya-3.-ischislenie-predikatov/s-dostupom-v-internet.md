---
description: 'Как работать с Прологом, если есть интернет'
---

# С доступом в Интернет

## Шаг 1. Переход к среде SWI-Prolog

Зайти на сайт [SWISH ](https://swish.swi-prolog.org/example/examples.swinb)и ознакомится со средой

![&#x418;&#x43D;&#x442;&#x435;&#x440;&#x430;&#x43A;&#x442;&#x438;&#x432;&#x43D;&#x430;&#x44F; &#x441;&#x440;&#x435;&#x434;&#x430; &#x440;&#x430;&#x431;&#x43E;&#x442;&#x44B; &#x441; Prolog - SWISH](../../.gitbook/assets/image%20%2816%29.png)

## Шаг 2. Создать блокнот для работы

Для этого необходимо создать новую вкладку нажав на ![](../../.gitbook/assets/image%20%288%29.png) 

Далее необходимо выбрать Notebook в качестве типа вкладки 

![&#x412;&#x44B;&#x431;&#x43E;&#x440; &#x442;&#x438;&#x43F;&#x430; &#x432;&#x43A;&#x43B;&#x430;&#x434;&#x43A;&#x438;](../../.gitbook/assets/image%20%2810%29.png)

## Шаг 3. Начать описывать правила/предикаты

В окне блокнота можно одновременно описывать факты базы данных и правила вычисления новых фактов, для этого используются ячейки различного типа. 

![&#x412;&#x43A;&#x43B;&#x430;&#x434;&#x43A;&#x430; &#x431;&#x43B;&#x43E;&#x43A;&#x43D;&#x43E;&#x442;&#x430;](../../.gitbook/assets/image%20%283%29.png)

Ячейки с правилами/фактами не имеют специального обозначения, ячейки с задачами для системы обозначены как ![](../../.gitbook/assets/image%20%289%29.png) и могут быть запущены. 

## Пример

Все люди смертны, Сократ человек, значит тоже смертен. 

![&#x41F;&#x440;&#x438;&#x43C;&#x435;&#x440; &#x440;&#x430;&#x431;&#x43E;&#x442;&#x44B; &#x441; &#x438;&#x43D;&#x442;&#x435;&#x440;&#x430;&#x43A;&#x442;&#x438;&#x432;&#x43D;&#x43E;&#x439; &#x441;&#x440;&#x435;&#x434;&#x43E;&#x439;](../../.gitbook/assets/image%20%2811%29.png)

В качестве факта в базе содержится информация о Сократе, как о человеке. Предикат "смертен" истинен только тогда, когда Х подставленный в качестве аргумента предиката одновременно является и человеком. 

Я мыслю, следовательно, существую

![&#x41F;&#x440;&#x438;&#x43C;&#x435;&#x440; &#x440;&#x430;&#x431;&#x43E;&#x442;&#x44B; &#x441; &#x438;&#x43D;&#x442;&#x435;&#x440;&#x430;&#x43A;&#x442;&#x438;&#x432;&#x43D;&#x43E;&#x439; &#x441;&#x440;&#x435;&#x434;&#x43E;&#x439;](../../.gitbook/assets/image%20%284%29.png)

В качестве фактов содержится некоторая информация. В качестве предикатов описаны правила вывода если некоторый Х мыслит, то значит и существует. И обратный предикат, если некоторый Х мыслит, то существует. 

