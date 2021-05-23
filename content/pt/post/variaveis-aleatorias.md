---
date: "2021-05-23"
description: "Apresentar o conceito variáveis aleatórias"
featured_image: https://images.unsplash.com/photo-1518186233392-c232efbf2373?ixid=MXwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHw%3D&ixlib=rb-1.2.1&auto=format&fit=crop&w=967&q=80
tags:
- probabilidade
title: 'Variáveis Aleatórias'
---

# Variáveis Aleatórias

## O que é uma variável aleatória?
Apesar do nome, variável aleatória, estamos mais interessados na função de probabilidade que será gerada. A variável aleatória associa cada resultado obtido de um experimento aleatório a um número. Veja o exemplo:

Assim, se o espaço amostral relativo ao "lançamento simultâneo de duas moedas de caras" que aparecem, a cada ponto amostral podemos associar um número para **X**, de acordo com a Tabela 10.1:

| **PONTO AMOSTRAL**    | **x**      |
| --------------------- |-----------:|
| (Ca, Ca)              | 2          |
| (Ca, Co)              | 1          |
| (Co, Ca)              | 1          |
| (Co, Co)              | 0          |

Se associarmos cada valor da variável aleatória com suas respectiva probabilidade, obtemos uma função de probabilidade

Essa função, asim definida, é denominada **função probabilidade** e representada por:

> f(x) = P(X = xi)

| **PONTO AMOSTRAL**    | **x**      | **P(X)**                     |
| --------------------- |:----------:|-----------------------------:|
| (Ca, Ca)              | 2          | 1/2 X 1/2 = 1/4              |
| (Ca, Co)              | 1          | 1/2 X 1/2 = 1/4              |
| (Co, Ca)              | 1          | 1/2 X 1/2 = 1/4              |
| (Co, Co)              | 0          | 1/2 X 1/2 = 1/4              |

## Outro exemplo

Se associarmos cada ponto de um dado a um número, obtemos a seguinte variável aleatória e função de probabilidade.

| **X**    | **P(X)**   |
| ---------|-----------:|
| 1        | 1/6        |
| 2        | 1/6        |
| 3        | 1/6        |
| 4        | 1/6        |
| 5        | 1/6        |
| 6        | 1/6        |
|          | ∑ = 1      |