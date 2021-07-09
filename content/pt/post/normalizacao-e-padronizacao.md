---
date: "2021-07-09"
description: "Uma das atividades do Pré-Processamento dos Dados é o redimensionamento dos dados. Nessa etapa a gente faz a Normalização ou Padronização dos dados, pois alguns algoritmos performam melhor quando os dados estão numa mesma escala."
featured_image: https://images.unsplash.com/photo-1515879218367-8466d910aaa4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80
tags:
- python
- pré-processamento-de-dados
title: 'Normalização e Padronização'
---

# Normalização

A normalização é boa para usar quando você sabe que a distribuição de seus dados não seguem uma distribuição Gaussiana. Isso pode ser útil em algoritmos que não assumem nenhuma distribuição de dados, como K-vizinhos mais próximos e redes neurais.

Uma das primeiras tarefas dentro do pré-processamento, é colocar seus dados na mesma escala. Muitos algoritmos de Machine Learning vão se beneficiar disso e produzir resultados melhores. Esta etapa também é chamada de normalização e significa colocar os dados em uma escala com range entre 0 e 1. Isso é útil para a otimizaçã, sendo usado no core dos algoritmos de Machine Learning, como gradiennt descent. Isso também é útil para algoritmos como regressão e redes neurais e algoritmos que usam medidas de distância, como KNN. O scikit-learn possui uma função para esta etapa, chamada MinMaxScaler().

```python
from pandas import read_csv
from sklearn.preprocessing import MinMaxScaler

arquivo = 'arquivo.csv'
dados = read_csv(arquivo)
array = dados.values

X = array[:,0:8]
Y = array[:,8]

scaler = MinMaxScaler(feature_range = (0,1))
rescaledX = scaler.fit_transform(X)

print("Dados Originais: \n\n", dados.values)
print("\nDados Normalizadoss: \n\n", rescaledX[0:5,:])
```

# Padronização

A padronização, por outro lado, pode ser útil nos casos em que os dados seguem uma distribuição gaussiana. No entanto, isso não precisa ser necessariamente verdade. Além disso, ao contrário da normalização, a padronização não tem um intervalo delimitador. Portanto, mesmo que você tenha valores discrepantes em seus dados, eles não serão afetados pela padronização

Padronização é a técnica para transformar os atributos com distribuição Gaussiana (normal) e diferentes médias e desvios padrão em uma distribuição Gausiana com média igual a 0 e desvio padrão igual a 1. Isso é útil para algoritmos que esperam que os dados estejam com uma distribuição Gaussiana, como regressão linear, regressão logística e linear discriminant analysis. Funciona bem quando os dados já estão na mesma escala. O scikit-learn possui uma função para esta etapa, chamada StandardScaler().

```python
from pandas import read_csv
from sklearn.preprocessing import StandardScaler

arquivo = 'arquivo.csv'
dados = read_csv(arquivo)
array = dados.values

X = array[:,0:8]
Y = array[:,8]

scaler = StandardScaler().fit(X)
standardX = scaler.transform(X)

print("Dados Originais: \n\n", dados.values)
print("\nDados Normalizadoss: \n\n", rescaledX[0:5,:])
```