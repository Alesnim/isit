---
description: 'Цель работы:'
---

# Практическая 7. Нечеткая кластеризация

## Теоретические сведения

**Кластерный анализ** \(англ. cluster analysis\) — многомерная статистическая процедура, выполняющая сбор данных, содержащих информацию о выборке объектов, и затем упорядочивающая объекты в сравнительно однородные группы. Задача кластеризации относится к статистической обработке, а также к широкому классу задач обучения без учителя.

Большинство исследователей склоняются к тому, что впервые термин «кластерный анализ» \(англ. cluster — гроздь, сгусток, пучок\) был предложен математиком Р. Трионом. Впоследствии возник ряд терминов, которые в настоящее время принято считать синонимами термина «кластерный анализ»: автоматическая классификация, ботриология.

Методы нечеткой классификации:

* Метод нечёткой кластеризации C-средних
* Метод основ 
* Метод основанный на энтропии

### Метод нечеткой классификации С-средних

**Метод нечёткой кластеризации C-средних** \(англ. fuzzy clustering, soft k-means, c-means\) позволяет разбить имеющееся множество элементов мощностью $$N$$ на заданное число нечётких множеств $$k$$. Метод нечеткой кластеризации C-средних можно рассматривать как усовершенствованный метод k-средних, при котором для каждого элемента из рассматриваемого множества рассчитывается степень его принадлежности \(англ. responsibility\) каждому из кластеров.

**Алгоритм:**

1. Задать случайным образом $$k$$ центров кластеров $$c_j, j = 1...k$$;

   1. Рассчитать матрицу принадлежности элементов к кластерам $$r$$ . В случае нормального распределения: 

   $$r_{ij}={\frac {{\mathcal {N}}(d(x_{i},c_{j})|\mu =0,\sigma )}{\displaystyle \sum _{j}^{k}{\mathcal {N}}(d(x_{i},c_{j})|\mu =0,\sigma )}}$$   
   , где $$x_i$$ — $$i-й$$ элемент множества, $$с_j$$ — центр кластера $$j$$, $$d(x_{i},c_{j})$$ — расстояние между точками $$x_i$$ и $$c_j$$ , $$\mathcal {N}$$ — плотность вероятности нормального распределения в точке $$d(x_{i},c_{j})$$ .

2. Переместить центры кластеров $$c_{j}\leftarrow {\frac {\displaystyle \sum _{i}r_{ij}x_{i}}{\displaystyle \sum _{i}r_{ij}}}$$ ;
3. Рассчитать функцию потерь \(например, исходя из принципа максимального правдоподобия\). В случае нормального распределения функция потерь будет равна: $$ J = \sum _{j}^{k}\sum _{i}^{N}d(x_{i},c_{j})^{2}r_{ij}$$ ;
4. Если значение функции потерь уменьшается, то повторить цикл с п.2.

Метод нечеткой кластеризации C-средних имеет ограниченное применение из-за существенного недостатка — невозможность корректного разбиения на кластеры, в случае когда кластеры имеют различную дисперсию по различным размерностям \(осям\) элементов \(например, кластер имеет форму эллипса\).

### Метод основанный на энтропии

Энтропия это величина определяющая меру схожести, основанная на евклидовом расстоянии. 

Чем ближе точка к центру кластера, тем меньше величина энтропии. 

**Алгоритм:**

1. Задать случайным образом $$k$$ центров кластеров $$c_j, j = 1...k$$;
2. Вычислить евклидово расстояние между $$i$$ и $$j $$ :  $$d_{ij} = \sqrt{\sum_{k=1}^{L}{(x_{ik} - x_{jk})^2}}$$ 
3. Вычислить меру схожести между двумя точками $$S_{ij} = e^{-\alpha d_{ij}}$$ 
4. Вычислить меру энтропии для всех точек: $$E = -Slog_2S - (1 -S)log_2(1-S)$$ 
5. Определяем общую меру энтропии для  $$x_i$$ относительно всех остальных данных: $$E_i = - \sum_{j \in x}^{j \neq i}{(S_{ij} log_2 S_{ij} + (1 - S_{ij} log_2 (1 - S_{ij})))}$$ 




