---
date: "2022-01-23"
description: "Métodos de amostragem para treinar os algoritmos de classificação/regressão"
featured_image: https://images.unsplash.com/photo-1529101091764-c3526daf38fe?ixid=MXwxMjA3fDB8MHxzZWFyY2h8MzF8fG1hY2hpbmUlMjBsZWFybmluZ3xlbnwwfHwwfA%3D%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=500&q=60
tags:
- machine learning
- python
title: 'Métodos de amostragem'
---

# Métodos de amostragem para treinar os algoritmos de classificação/regressão.

![](https://miro.medium.com/max/1000/0*VM360JmLber68J71.gif)

A abordagem mais simples é o holdout: separar os dados uma única vez entre conjuntos de treino e teste. Por exemplo: 80% dos exemplos para treinamento do algoritmo, e 20% para teste. Essa alternativa é comumente utilizada quando trabalha-se com uma grande quantidade de dados e a distribuição dos padrões não se diferencia entre possíveis amostras de treino e teste. 

Entretanto, quando temos conjuntos de dados de tamanho médio e pequeno, pode ocorrer uma grande variância nos resultados dos algoritmos. Isso ocorre porque ao se dividir os conjuntos de treino/teste, a distribuição dos dados fica disforme, implicando em diferentes resultados cada vez que se repete o programa. Uma estratégia para reduzir esse efeito é realizar a validação cruzada (cross validation), dividindo os dados em K várias partições e permutá-las ao avaliar os modelos induzidos. Ou seja, treinar sempre com K-1 partições e avaliar na partição remanescente. Assim, repete-se K vezes, até que todas as partições tenham sido usadas como teste. O desempenho final é a media das K repetições.

Ainda, se o conjunto for extremamente pequeno, é possível usar o "leave one out" (deixar um fora, literalmente). É uma validação cruzada onde a quantidade de partições é igual ao número de exemplos (linhas) do dataset. Em cada iteração treina-se o algoritmo com N-1 linhas, e realiza a predição do exemplo separado para teste. Ao contrário das outras técnicas, aqui temos como retorno a predição individual de cada exemplo, que devem ser agregadas e calculadas por meio da métrica/medida de desempenho selecionada.

## Holdout

![](https://d1m75rqqgidzqn.cloudfront.net/wp-data/2020/07/15185319/blogs-15-7-2020-02-1024x565.jpg)


Aqui está o código Python que pode ser usado para criar a divisão de treinamento e teste do conjunto de dados original.  No código abaixo, o conjunto de dados de habitação do Sklearn Boston é usado para demonstrar como o método train_test_split de Sklearn.model_selection pode ser usado para dividir o conjunto de dados em conjunto de dados de treinamento e teste.  Observe que o tamanho do teste é mencionado usando o parâmetro test_size.


```python
from sklearn import datasets
from sklearn.model_selection import train_test_split

bhp = datasets.load_boston()

X_train, X_test, y_train, y_test = train_test_split(bhp.data, bhp.target, random_state=42, test_size=0.3)
```

## Validação cruzada (cross validation)

![](https://d1m75rqqgidzqn.cloudfront.net/wp-data/2020/07/15185337/blogs-15-7-2020-01-1024x565.jpg)

No código abaixo, utilizamos a classe KFold do sklearn para criar fold dividindo os dados 3 vezes. O método split retorna os indices dos dados para treino e teste para cada iteração


```python
from sklearn import datasets
from sklearn.model_selection import KFold
import numpy as np

rn = range(1,26)

kf3 = KFold(n_splits=3, shuffle=False)

for train_index, test_index in kf3.split(rn):
    print(train_index, test_index)
```

    [ 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24] [0 1 2 3 4 5 6 7 8]
    [ 0  1  2  3  4  5  6  7  8 17 18 19 20 21 22 23 24] [ 9 10 11 12 13 14 15 16]
    [ 0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15 16] [17 18 19 20 21 22 23 24]
    

## Leave one out

![](https://miro.medium.com/max/607/1*SGNQoJtwG7YTcx7TRpUkGg.png)

No código abaixo, cada amostra é usada uma vez como um conjunto de teste, aplicando o método split da classe LeaveOneOut do pacote sklearn.model_selection. As amostras restantes formam o conjunto de treinamento.


```python
import numpy as np
from sklearn.model_selection import LeaveOneOut
X = np.array([[1, 2], [3, 4], [5, 6], [7, 8], [9, 0]])
y = np.array([1, 2, 3, 2, 2])
loo = LeaveOneOut()
loo.get_n_splits(X)

for train_index, test_index in loo.split(X):
    print("TRAIN:", train_index, "TEST:", test_index)
    X_train, X_test = X[train_index], X[test_index]
    y_train, y_test = y[train_index], y[test_index]
```

    TRAIN: [1 2 3 4] TEST: [0]
    [[3 4]
     [5 6]
     [7 8]
     [9 0]] [[1 2]] [2 3 2 2] [1]
    TRAIN: [0 2 3 4] TEST: [1]
    [[1 2]
     [5 6]
     [7 8]
     [9 0]] [[3 4]] [1 3 2 2] [2]
    TRAIN: [0 1 3 4] TEST: [2]
    [[1 2]
     [3 4]
     [7 8]
     [9 0]] [[5 6]] [1 2 2 2] [3]
    TRAIN: [0 1 2 4] TEST: [3]
    [[1 2]
     [3 4]
     [5 6]
     [9 0]] [[7 8]] [1 2 3 2] [2]
    TRAIN: [0 1 2 3] TEST: [4]
    [[1 2]
     [3 4]
     [5 6]
     [7 8]] [[9 0]] [1 2 3 2] [2]
    
