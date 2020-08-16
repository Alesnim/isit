---
description: Как работать с Прологом если нет доступа в Интернет
---

# Если нет интернета

## Шаг 1. Скачать/установить SWI-Prolog

Установить среду SWI-Prolog

## Шаг 2. Запустить SWI-Prolog

![&#x41D;&#x430;&#x447;&#x430;&#x43B;&#x44C;&#x43D;&#x43E;&#x435; &#x43E;&#x43A;&#x43D;&#x43E; &#x43A;&#x43E;&#x43D;&#x441;&#x43E;&#x43B;&#x438; SWI-Prolog](../../.gitbook/assets/image%20%2812%29.png)

При запуске графической версии запускается консоль для работы с машиной Пролог. 

## **Шаг 3. Создать новую программу**

Для создания новой программы можно воспользоваться **File -&gt; New ...**

![&#x41E;&#x43A;&#x43D;&#x43E; &#x440;&#x435;&#x434;&#x430;&#x43A;&#x442;&#x43E;&#x440;&#x430; &#x43F;&#x440;&#x43E;&#x433;&#x440;&#x430;&#x43C;&#x43C;&#x44B; SWI-Prolog](../../.gitbook/assets/image%20%2813%29.png)

В окне редактора описываются правила и факты программы. 

## Шаг 4. Запуск программы

Для запуска программы необходимо войти в режим консультации в окне консоли SWI-Prolog. **File -&gt; Consult ...**

![&#x41E;&#x43A;&#x43D;&#x43E; &#x43A;&#x43E;&#x43D;&#x441;&#x43E;&#x43B;&#x438; &#x432; &#x440;&#x435;&#x436;&#x438;&#x43C;&#x435; &#x43A;&#x43E;&#x43D;&#x441;&#x443;&#x43B;&#x44C;&#x442;&#x430;&#x446;&#x438;&#x438;](../../.gitbook/assets/image%20%2815%29.png)

Теперь возможно описание целей для вычислений.

## Пример

Все люди смертны, Сократ человек, значит тоже смертен. 

![&#x41B;&#x438;&#x441;&#x442;&#x438;&#x43D;&#x433; &#x43F;&#x440;&#x43E;&#x433;&#x440;&#x430;&#x43C;&#x43C;&#x44B; ](../../.gitbook/assets/image%20%285%29.png)

![&#x41E;&#x442;&#x432;&#x435;&#x442; &#x43F;&#x440;&#x43E;&#x433;&#x440;&#x430;&#x43C;&#x43C;&#x44B; &#x432; &#x440;&#x435;&#x436;&#x438;&#x43C;&#x435; &#x43A;&#x43E;&#x43D;&#x441;&#x443;&#x43B;&#x44C;&#x442;&#x430;&#x446;&#x438;&#x438;](../../.gitbook/assets/image%20%287%29.png)

В качестве факта в базе содержится информация о Сократе, как о человеке. Предикат "смертен" истинен только тогда, когда Х подставленный в качестве аргумента предиката одновременно является и человеком. 

Я мыслю, следовательно, существую

![&#x41B;&#x438;&#x441;&#x442;&#x438;&#x43D;&#x433; &#x43F;&#x440;&#x43E;&#x433;&#x440;&#x430;&#x43C;&#x43C;&#x44B;](../../.gitbook/assets/image%20%286%29.png)

![&#x41E;&#x442;&#x432;&#x435;&#x442;&#x44B; &#x43F;&#x440;&#x43E;&#x433;&#x440;&#x430;&#x43C;&#x43C;&#x44B; &#x432; &#x440;&#x435;&#x436;&#x438;&#x43C;&#x435; &#x43A;&#x43E;&#x43D;&#x441;&#x443;&#x43B;&#x44C;&#x442;&#x430;&#x446;&#x438;&#x438;](../../.gitbook/assets/image%20%282%29.png)

В качестве фактов содержится некоторая информация. В качестве предикатов описаны правила вывода если некоторый Х мыслит, то значит и существует. И обратный предикат, если некоторый Х мыслит, то существует. 
