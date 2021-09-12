---
date: "2021-06-20"
description: "O Python providencia um padrão, conhecido como Python DB-API, para acesso aos mais variados Bancos de Dados (BDs)."
featured_image: https://images.unsplash.com/photo-1555952494-efd681c7e3f9?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=750&q=80
tags:
- python
- banco de dados
title: 'Banco de Dados com Python'
---

# Banco de Dados com Python

O Python providencia um padrão, conhecido como Python DB-API, para acesso aos mais variados
Bancos de Dados (BDs). Os principais elementos do Python DB-API são:

- Função **connect** : uma função usada para conectar a um BD e que retorna um **objeto de**
    **conexão** ;
- **Objeto de conexão** : representa uma conexão com um BD. Este objeto de conexão provê
    acesso a um **cursor de objetos** ;
- **Cursor de objetos** : é usado para executar comandos ou consultas SQL, após a execução de
    uma consultas haverá o **resultado de uma execução** no próprio cursor;
- **Resultado de uma execução** : São os resultados de uma execução de um comando SQL.
    Se o comando for uma consulta (i.e., **SELECT** ) o resultado sera um tipo de sequencia de
    sequencias (como uma tupla de tuplas).

### 2 Preparando o ambiente para uso com PostgreSQL

Neste material realizaremos um exemplo prático com PostgreSQL, e assumiremos os seguintes
detalhes sobre o seu ambiente:

- Você deve ter um servidor PostgreSQL instalado e rodando (neste material usamos o Post-
    greSQL versão 12);
- Você deve ter instalado o pacote psycopg2, instale conforme seu ambiente, exemplos:
    **-** pip (terminal): pip install psycopg
    **-** conda (terminal): conda install psycopg
    **-** Anaconda (interface):
       ∗ Em ambientes (environments) selecione um ambiente (padrão: base(root));
       ∗ Clique em ‘atualizar índice...’/‘update index...’;
       ∗ Selecione ‘todos’/‘all’ ou ‘não instalados’/‘not installed’;
       ∗ Procure e selecione o pacote ‘psycopg2’; e
       ∗ Clique em ‘Aplicar’/‘Apply’.
- Nos exemplos abaixo consideramos:
    **-** Um servidor PostgreSQL na máquina local ‘localhost’ na porta padrão;
    **-** Neste servidor há um banco (dbname) ‘poscd’; e
    **-** Acessamos com o usuário(user) ‘postgres’ e senha ‘postgres15’.

**Altere conforme a configuração da sua máquina.**


### 3 Python DB-API (como implementada pelo psycopg2)

- **connect** : Conecta a um banco de dados

#### 3.1 Objeto de conexão


O Objeto de conexão , obtido por connect , provê os seguintes métodos:

- **cursor** : retorna um cursor;
- **commit** : efetiva as transações pendentes no BD. Por padrão, ao criar um cursor, o psycopg
    cria uma transação. Se **commit** não for chamado, qualquer manipulação realizada será
    perdida;
- **rollback** : descarta todas as transações pendentes do cursos, desde o último **commit** ;
- **close** : fecha a conexão. Fechar uma conexão sem antes chamar commit vai forçar um **rollback**
    nas transações pendentes.

#### 3.2 Cursor


Os principais métodos de um cursor são:

- **execute(query, vars=None)** : executa uma operação (comando ou consulta) definido pela
    string **query**. Parâmetros podem ser providenciados em **vars** tanto como uma sequencia
    (e.g. list) ou um mapa (e.g. dict). Na query você pode referencias os parâmetros de um
    sequencia com **%s** e os de um mapa com **%(nome)s**. O método retorna **None** , você pode
    iterar pelo cursos para obter os resultados.
- **executemany(query, vars_list)** : executa a operação para cada conjunto de valores
    definidos por **vars_list**. Resultados retornados são descartados.
- **fetchmany(size)** : retorna os **size** resultados de uma consulta
- **close** : fecha o cursor.

### 4 Importar o pacote/biblioteca ‘psycopg2’

```python
import psycopg
```

### 5 Criar uma conexão e um cursor

```python
conn =psycopg2.connect("dbname=poscd user=postgres password=postgres15")
cur =conn.cursor()
```

### 6 Executar comandos SQL


Agora podemos utilizar o cursor para executar consultas SQL. Passamos a consulta ( query ) como
primeiro argumento do método cur.execute.
A consulta abaixo cria uma tabela, observe que usamos IF NOT EXISTS para prevenir o erro
de tentar criar uma tabela que já existe.

```python
cur.execute("CREATE TABLE IF NOT EXISTS mensagem (id serial PRIMARY KEY,
prioridade integer, titulo varchar, corpo varchar);")
```

### 7 Consultas com parâmetros/argumentos


Nunca se deve adicionar valores/parâmetros diretamente na string, query , da consulta. Princi-
palmente se esses valores pode ser manipulados pelo usuário! Um usuário malicioso poderia se
aproveitar disso e injetar algum comando SQL malicioso.
O método execute aceita um segundo argumento que pode ser um contêiner sequencial (tupla,
lista) ou um mapa (dicionário). Na query referenciamos estes argumentos posicionais com %s e
os de um mapa com %(nome)s.

```python
cur.execute("INSERT INTO mensagem (prioridade, titulo, corpo) VALUES ( %s , %s ,
%s)", ( 100 , "Yuri's","Minha mensagem"))
```


Observe que não passamos o campo id , pois por ser do tipo serial ele é automaticamente preenchido
em ordem crescente pelo PostgreSQL. Os três %s são casados em ordem com os valores da tupla.
Vamos agora efetivar as alterações com commit , concluindo a transação. Depois fechamos o cursor
e conexão; os quais não poderão mais ser utilizados.

```python
conn.commit()
cur.close()
conn.close()
```

### 8 Nome dos argumentos


Abaixo criamos uma outra tabela, chat. Nela temos dois campos de data ( date ): ‘criada’ e
‘atualizada’.
Quando inserimos queremos que ambos tenham a mesma data. Não necessitamos passar o mesmo
valor duas vezes, podemos passar um dicionário e referenciar a mesma chave do dicionários várias
vezes na query.

```python
import psycopg
import datetime
```

```python
conn =psycopg2.connect("dbname=poscd user=postgres password=postgres15")
cur =conn.cursor()
cur.execute("CREATE TABLE IF NOT EXISTS chat (id serial PRIMARY KEY, prioridade
integer, texto varchar, criada date, atualizada date);")
```

```python
cur.execute("""INSERT INTO chat (prioridade, texto, criada, atualizada)
VALUES ( %(numprioridade)s , %(msg)s , %(data)s , %(data)s );""",
{'numprioridade': 10 , 'msg': "Olá, tudo bem?", 'data': datetime.
date( 2020 , 8 , 5 )})
conn.commit()
```

```python
cur.close()
```

### 9 Buscando dados (consulta)


Primeiro vamos criar uma conexão e cursor.

```python
conn =psycopg2.connect("dbname=poscd user=postgres password=postgres15")
cur =conn.cursor()
```


Vamos inserir mais dados na tabela chat.
Observe que utilizamos executemany e como segundo argumento passamos uma lista de di-
cionários ( dados ), cada dicionário será uma nova entrada (registro) na tabela. Para cada elemento
em dados (que é um dicionário) será executado uma query.


```python
dados= [
{'numprioridade': 15 , 'msg':"Tudo bem e você?", 'data': datetime.
date( 2020 , 7 , 6 )},
{'numprioridade': 5 ,'msg':"Estou bem também, obrigado.", 'data': datetime.
date( 2020 , 7 , 6 )},
{'numprioridade': 100 , 'msg': "Não esqueça de fazer os questionários da
disciplina", 'data': datetime.date( 2020 , 7 , 6 )},
]
cur.executemany("""INSERT INTO chat (prioridade, texto, criada, atualizada)
VALUES ( %(numprioridade)s , %(msg)s , %(data)s , %(data)s );""", dados)
conn.commit()
```


Abaixo executamos uma consulta (SELECT), usamos o mesmo cursor já criado (e usado para
inserir dados) já que ainda não fechamos ele.
Após a consulta simplesmente iteramos pelo cursor, a cada iteração temos um registro da tabela,
conforme a consulta.

```python
cur.execute('SELECT * FROM chat')
for k in cur:
print(k)
```

```python
(1, 10, 'Olá, tudo bem?', datetime.date(2020, 8, 5), datetime.date(2020, 8, 5))
(2, 15, 'Tudo bem e você?', datetime.date(2020, 7, 6), datetime.date(2020, 7,
6))
(3, 5, 'Estou bem também, obrigado.', datetime.date(2020, 7, 6),
datetime.date(2020, 7, 6))
(4, 100, 'Não esqueça de fazer os questionários da disciplina',
datetime.date(2020, 7, 6), datetime.date(2020, 7, 6))
```

Podemos utilizar todas as vantagens do SQL para filtrar nossas consultas, veja o exemplo abaixo:

```python
cur.execute('SELECT * FROM chat WHERE prioridade <= 10')
for k in cur:
```


```python
print(k)
```

```python
(1, 10, 'Olá, tudo bem?', datetime.date(2020, 8, 5), datetime.date(2020, 8, 5))
(3, 5, 'Estou bem também, obrigado.', datetime.date(2020, 7, 6),
datetime.date(2020, 7, 6))
```

O cursor pode nos trazer várias informações relevantes, observe:

```python
cur.execute('SELECT * FROM chat')
print("rowcount", cur.rowcount) _# número de registros da última consulta_
print(cur.description) _# Uma série de meta informações de cada coluna da_última consulta_
rowcount 4
(Column(name='id', type_code=23), Column(name='prioridade', type_code=23),
Column(name='texto', type_code=1043), Column(name='criada', type_code=1082),
Column(name='atualizada', type_code=1082))
```

Finalmente fechamos o cursor e a consulta.

```python
[12]: cur.close()
conn.close()
```

### 10 Referências
Comunidade Psycopg. Psycopg – PostgreSQL database adapter for Python. Disponível em
https://www.psycopg.org/docs/.

John Hunt. Advanced Guide to Python 3 Programming. Undergraduate Topics in Computer
Science. Springer, 2019.


