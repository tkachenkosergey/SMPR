
Задачи классификации
=====================
Метрические алгоритмы классификации
-----------------------------------
Метрический алгоритм - алгоритм классификации основанный на оценке сходства объектов.Для формализации понятия сходств, вводится *функция расстояния* в простанстве объектов X, то есть, чем меньше расстояние, тем больше объекты похожи друг на друга. При этом метрические алгоритмы основываются на гипотезе компактности, которая говорит, что *схожим объектам соответствуют схожие ответы*.

Алгоритм k ближайших соседей (KNN)
----------------------------------
Имеется некоторая выборка Xl, состоящая из объектов x(i), i = 1, ..., l(выборка ирисов Фишера). **Алгоритм KNN** относит классифицируемый объект *z* к тому классу , к которому относится большинство из k его ближайших соседей.
```R
kNN <- function(xl, z, k)
{
  ## Сортируем выборку согласно классифицируемого объекта
  orderedXl <- sortObjectsByDist(xl, z)
  n <- dim(orderedXl)[2] - 1
  
  ## Получаем классы первых k соседей
  classes <- orderedXl[1:k, n + 1]
  
  ## Составляем таблицу встречаемости каждого класса
  counts <- table(classes)
  ## Находим класс, который доминирует среди первых k соседей
  class <- names(which.max(counts))
  
  return (class)
}
```
**Результат работы**

![knn](https://user-images.githubusercontent.com/43620917/47822651-e94f4a80-dd75-11e8-879f-0825d5ff65d8.png)

Алгоритм 1NN
------------
Преимущество алгоритма 1NN-просто реализации. В отличии от kNN,алгоритм 1NN относит классифицируемый объект z к тому классу, к которому относится его ближайший сосед.
 
Пусть задана выборка Xl, состоящая из объектов x(i), i = 1, ..., l(выборка ирисов Фишера) и классифицируемый объект z.
Затем подбирается метрика, в данном случае используется евклидово расстояние.

```R
euclideanDistance <- function(u, v){ 
  return(sqrt(sum((u - v)^2)))
}
```
Далее сортируем объекты в порядке увеличения расстояния  относительно заданой точке и  тогда заданая точка будет принадлежать классу элемента стоящего первый в отсортированном списке.

```R
 for (i in 1:l){
    tmp_dist =metricFunction(xl[i, 1:n], z)
    
    if(tmp_dist < min_dist) {
      min_dist = tmp_dist
      min_dist_class = xl[i, n+1]
    }
  }
  
  return (min_dist_class)
}
```
**Задачи классификации 1NN**

![1nn](https://user-images.githubusercontent.com/43620917/47834525-dd34ae80-ddb0-11e8-8137-c4348e4a2d04.png)

LOO
---------
Суть LOO состоит в том, что мы из выборки удаляем элемент, алгоритм обучается на полученной выборке. Затем обученный алгоритм проверяется на исключенном элементе. Таким образом поступаем со всеми элементами выборки. После чего можно оценить метод обучения  по частоте ошибочный классификаций.


KWNN
--------



Байесовские	алгоритмы	классификации
-----------------------------------
Байесовский подход опирается на теорему о том, что если плотности распределения классов известны, то алгоритм классификации имеюий минимальную вероятность ошибок можно выписать в явном виде.

Для того чтобы классифицировать точку,нужно вычислить функции правдоподобия каждого из классов, по ним вычисляются апостериорные вероятности классов.  Объект будет  относится к тому классу, у которого апостериорная вероятность максимальна.

![default](https://user-images.githubusercontent.com/43620917/50468020-b30d0080-099d-11e9-9123-70b78be63eb1.png)

Наивный байесовский классификатор
---------------------------------

Наивный байесовский классификатор-простой вероятностный классификатор, основанный на применении теоремы Байеса со строгими (наивными) предположениями о независимости. 


**Результат работы**


![default](https://user-images.githubusercontent.com/43620917/50468056-dd5ebe00-099d-11e9-8757-491ee21dbc53.png)






  
   
 



