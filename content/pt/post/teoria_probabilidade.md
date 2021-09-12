---
date: "2021-03-25"
description: "Conceitos  bases  de  teoria  de probabilidades"
featured_image: https://images.unsplash.com/photo-1518186233392-c232efbf2373?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=967&q=80
tags:
- probabilidade
title: 'Teoria da probabilidade'
---



# O que é e por que estudar probabilidades?

O primeiro argumento vem do fato de que o mundo é muito mais “probabilístico” do que “determinístico”.

Por exemplo: é muito mais plausível dizer que tem uma chance de 75% de chover hoje do que afirmar com toda a certeza que irá chover.

Entender probabilidades é entender como o mundo funciona: isso nos ajuda nas tomadas de decisões!

# Mais fácil falar do que fazer...

Existem situações simples de prever. Pense no lançamento de uma moeda, por exemplo.

Mas  existem  situações  complicadíssimas  de  determinar  como,  por exemplo,  qual  a  probabilidade  de  uma  pessoa  ser  atropelada  por  uma limousine prata no cruzamento das ruas Brigadeiro Franco com a Av. Sete de Setembro

# Definição: Experimento Aleatório

Um experimento aleatório é um experimento em que não possível afirmar com CERTEZA o resultado. 

Ou seja, não é DETERMINÍSTICO, mas sim, PROBABILÍSTICO.

Exemplos: 
- Lançamento de uma moeda
- Lançamento de dados
- Retirada de uma bola em uma urna fechada cheia de outras bolas
- Resultado das eleições
- Resultado da mega-sena

# Definição: Evento

Um evento é um possível resultado de um experimento aleatório.

Por exemplo, um evento possível do resultado da mega-sena, é o seguinte: {(32, 16, 24, 12, 18, 48)}

Um evento possível do lançamento de duas moedas:{(CARA, COROA)}

Um evento possível do lançamento de três dados{(1, 6, 6)}

# Definição: Espaço Amostral (Ω)

Todos os eventos possíveis é o que compõe o espaço amostral.

Exemplo: tome o experimento aleatório de jogar uma moeda 3 vezes

Quantos elementos terá o espaço amostral?

Um evento E1 poderia ser = {(Ca, Ca, Co)}

Um evento E2 poderia ser = {(Co, Ca, Co)}....

Quantos destes teremos?

É aqui que “truques” de contagem e análise combinatória são úteis

Pense da seguinte maneira:

No primeiro lançamento, são apenas dois resultados possíveis: Ca ou Co

O mesmo se repete para o segundo e para o terceiro lançamento.

Logo o número de eventos total é: 2 . 2 . 2 = 8

Escrito de modo formal: n(Ω) = 8

# Definição clássica de Probabilidades

A probabilidade de um evento “A” acontecer, em um espaço amostral (Ω)É obtida por:
````
n(A) / n(Ω)
````

Em português: número de elementos de A divididos pelo número de elementos do espaço amostral inteiro

# Exemplo I

Qual a probabilidade de retirar um três de ouros de um baralho?

Obs.: um baralho possui 52 cartas. O três de ouros é 1 carta destas 52.

Logo o evento A = tirar um três de ouros tem apenas 1 elemento, pois só tem um três de ouros no baralho.

Já o espaço amostral tem 52 elementos, é um número total de cartas do baralho.

A probabilidade será, portanto: 1/52 ou 1,923%

# Exemplo II

Qual a probabilidade de retirar duas caras seguidas ao lançar uma moeda duas vezes?

Da uma olhada no espaço amostral

Ω = {(Ca, Ca); (Ca, Co); (Co, Ca); (Co, Co)}

Agora dá uma olhada no evento que queremos que aconteça:

A = {(Ca, Ca)}

Ω = {(Ca, Ca); (Ca, Co); (Co, Ca); (Co, Co)}

O número de elementos do espaço amostral é = 4

A = {(Ca, Ca)}

O número de elementos do evento A é = 1

Logo a probabilidade vai ser ¼ ou 25%

# Definições adicionais

### Evento Certo: 
É um evento com probabilidade 100%
Por exemplo: qual a probabilidade de rolar um dado e tirar 1, 2, 3, 4, 5 ou 6?

### Evento Impossível:
É um evento que tem 0% de chance de acontecer
Por exemplo: qual a probabilidade de tirar um 7 ao rolar um dado de 6 faces enumerados de 1 a 6?
Outro exemplo: qual a probabilidade de chover cenouras prateadas dentro de um Fiat Uno 2007 preto a uma velocidade de 240 km/h?

### Eventos Complementares:
Por exemplo: retirar uma bolinha azul e retirar uma bolinha vermelha, de uma caixa que só tem bolinhas azuis e vermelhas.
O legal disso é que, sabendo que a probabilidade de tirar bolinhas azuis é 20%, podemos automaticamente dizer que probabilidade de tirar bolinhas vermelhas é 80%.

# Eventos mutuamente exclusivos

Se os eventos são mutuamente exclusivos, ou seja, eles NÃO TEM ELEMENTOS EM COMUM, a probabilidade da união deles, ou seja, de um OU outro ocorrer é igual a:
````
P(A∪B)= P(A) + P(B)
````

# Eventos com elementos na interseção

Se contarmos o número de elementos de A e somarmos ao número de elementos de B, estaremos contando duas vezes os elementos que estão na interseção.

É necessário, portanto, retirar o número de elementos que estão na interseção, pois contamos eles duas vezes!
```
n(A∪B) = n(A) + n(B) - n(A∩B) 
```

### Exemplo

Qual a probabilidade de obter “cara” no primeiro lançamento OU “coroa” no terceiro lançamento de uma moeda?

Cara no primeiro lançamento: {(Ca, Ca, Ca), (Ca, Ca, Co), (Ca, Co, Ca), (Ca, Co, Co)}

Coroa no terceiro lançamento:{(Ca, Ca, Co), (Ca, Co, Co), (Co, Ca, Co), (Co, Co, Co)}

Elementos da Interseção:{(Ca, Ca, Co), (Ca, Co, Co)}

Número de elementos do espaço amostral: 8

### Resolução

````
n(A∪B) = n(A) + n(B) - n(A∩B) 

n(A∪B)  = 4 + 4 -2 = 6

P(A∪B) = 6 / 8 = 75%
````

# Eventos Independentes
Dizemos que dois eventos são independentes quando a ocorrência de um dos eventos não altera a probabilidade de outro evento acontecer

Exemplo:
Uma caixa possui 2 bolinhas vermelhas e 3 bolinhas azuis. Iremos retirar uma bolinha da caixa aleatoriamente, repondo a bola após anotar sua cor.

Note que: 
se retirarmos duas bolas, o evento de tirar a primeira bola é independente de retirar a segunda bola.
```
P(A∩B) = P(A).P(B)
```

### Exemplo:

Qual a probabilidade de retirar uma “coroa” e em seguida uma “cara” ao lançar uma moeda?

O evento “coroa” e “cara” são independentes: um não altera a probabilidade do outro

Logo:

````
P(A∩B) = P(A).P(B) = 1/2.1/2 = 1/4
````

# Eventos Dependentes

Dizemos que dois eventos são dependentes quando a ocorrência de um dos eventos ALTERA a probabilidade dos demais eventos ocorrerem.

Exemplo:
Uma caixa possui 2 bolinhas vermelhas e 3 bolinhas azuis. Iremos retirar uma bolinha da caixa aleatoriamente, sem repor a bolinha.

Note que: 
se retirarmos duas bolas, o evento de tirar a primeira bola irá alterar a probabilidade de retirar a segunda bolinha.

```
P(A∩B) = P(A).P(A|B)
```
Lemos: probabilidade de B ocorrer dado que A ocorreu

### Exemplo:

Em uma caixa com 10 bolinhas vermelhas,10 bolinhas azuis, 5 bolinhas amarelas e 12 bolinhas verdes, qual a probabilidade de retirar uma bolinha amarela e em seguida uma vermelha (sem reposição)?

O evento “retirar bolinha amarela” e o evento “retirar bolinha vermelha” são DEPENDENTES, pois não tem reposição das bolinhas. Dessa forma, a probabilidade é calculada:

O espaço amostral tem 37 bolinhas.A probabilidade de retirar uma bolinha amarela, é, portanto:

````
P(Amarela) = 5/37
````

Já a probabilidade de retirar uma bolinha vermelha, dado que uma bolinha amarela foi retirada, é:

````
P(Amarela|Vermelha) = 10/36
````

Logo:

````
P(Amarela∩Vermelha) = 5/37.10/36
````