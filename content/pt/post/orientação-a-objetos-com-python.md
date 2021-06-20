---
date: "2021-06-06"
description: "A Orientação a Objetos (OO) é um paradigma de programação que estrutura uma aplicação deforma que os dados e as operações sobre estes dados são mantidas juntas em classes e acessadasvia objetos."
featured_image: https://images.unsplash.com/photo-1515879218367-8466d910aaa4?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=1050&q=80
tags:
- python
- orientação a objetos
title: 'Orientação a Objetos com Python'
---

# Orientação a Objetos

# Introdução

A Orientação a Objetos (OO) é um paradigma de programação que estrutura uma aplicação de forma que os dados e as operações sobre estes dados são mantidas juntas em classes e acessadas via objetos.  Outro tipo de paradigma de programação muito conhecido é o funcional, utilizado para criar programas na linguagem de programação R; muitas das features do paradigma funcional também estão disponível no Python.

Por  exemplo,  um  aluno  pode  ser  representado  por  uma  classe Aluno que  tem  vários  campos(atributos) como nome, código (id), data de nascimento, etc.  Várias operações (métodos) podem ser associadas: aprovar(), matricular(), retornar_grade_de_horario().

# Classes

Vários tipos de dados em Python que como inteiros, string e booleanos são objetos que armazenamum único item de dado. Porém, podemos fazer classes que armazenem um conjunto de dados que, em conjunto, representam algum objeto complexo como uma pessoa, aluno, empregado, etc.

## Classes padrões

Como visto anteriormente, os tipos de dados em Python são classes e cada valor um objeto (dize-mos que o objeto é a instância de uma classe).
Usamos **type()** para descobrir o tipo/classe de um objeto.

```python
print(type(2))
print(type(3.3))
print(type(True))
print(type('Texto'))
print(type([1, 2, 3, 4]))
```

Podemos usar is instance para descobrir se um determinado valor ou variável é de uma determinada classe/tipo:

```python
x = 42

if isinstance(x, int):
    print("É inteiro!")
    
if isinstance(x, float):
    print("É float????")
else:
    print("Não é float!")
```
É inteiro!
Não é float!

## Criando classes

O código abaixo cria uma classe Aluno com vários atributos.

A função__init__ é a função de inicialização de um objeto da classe, ela recebe pelo menos um parâmetro, self que é o objeto sendo criado.

```python
class Aluno:
    def __init__(self):
        self.nome = "-x-"
        self.id = -1
        self.curso = None

# criando um objeto do tipo aluno        
aluno = Aluno()
print(aluno)
print(aluno.nome)
print(aluno.id)
print(aluno.curso)
```

Observe como fazemos para instanciar um objeto.  Primeiro definimos um nome para o objeto. Nesse caso usamos o nome aluno. Após isso há o sinal de atribuição (=) e por fim,  o nome da classe seguido dos parenteses. Ficando:

aluno = Aluno()

Observe também como acessamos os atributos de um objeto. Utilizamos o nome do objeto (nesse caso  aluno)  seguindo de um ponto (.) e o atributo  que  queremos  acessar. Por  exemplo,  para acessar o valor nome, usamos:

aluno.nome

##  Argumentos para a inicialização

O método__init__aceita receber argumentos, veja:

```python
class Aluno:
    def __init__(self, nome, id_aluno=-1, curso=None):
        """nome é um argumento obrigatório, os demais são opcionais (há valor␣↪→padrão)"""
        self.nome = nome
        self.id = id_aluno
        self.curso = curso
        
# criando um objeto do tipo aluno
aluno = Aluno("Pedro")
print(aluno)
print(aluno.nome)
print(aluno.id)
print(aluno.curso)
```

Observe que toda vez que instanciamos um objeto, fazemos uma chamada ao método __init__.

Dessa forma, fazemos a passagem de parâmetros ao instanciar o objeto.

## __str__

Métodos com o nome iniciando e terminando com duas linhas (__) são métodos especiais. Um deles, **__str__**, nos permite definir a string a ser impressa quando imprimimos um objeto dessa classe.

```python
class Aluno:
    def __init__(self, nome, id_aluno=-1, curso=None):
        """nome é um argumento obrigatório, os demais são opcionais (há valor␣↪→padrão)"""
        self.nome = nome
        self.id = id_aluno
        self.curso = curso
        
    def __str__(self):
        return "Aluno (" + self.nome + ": " + str(self.id) + ")"

# criando um objeto do tipo aluno
aluno = Aluno("Pedro")
print(aluno)
```

Observe que a função **__srt__** formata como serão apresentados os valores dos atributos de um objeto da classe Aluno.

##  Criando objeto

Como visto acima, podemos instanciar uma classe por meio de um objeto. Na verdade, podemos criar quantos objetos de uma mesma classe forem necessários.

```python
a1 = Aluno("João", 1)
a2 = Aluno("Maria", 2)

print(a1, "::", a2)
```

Aluno (João: 1) :: Aluno (Maria: 2)

Cuidado com atribuições, veja no exemplo abaixo que a1 e a “apontam” para o mesmo objeto.

Observe também que podemos acessar diretamente os atributos de um objeto. No exemplo abaixo,modificamos o atributo nome.

```python
a = a1
print(a1)
a.nome = "Pedro"
print("a:", a)
print("a1: ", a1)
```
Aluno (João: 1)
a: Aluno (Pedro: 1)
a1:  Aluno (Pedro: 1)

##  Comentário da classe (docstring)

O exemplo abaixo mostra como documentar uma classe

```python
class Aluno:
    """Esta classe representa um aluno,possui nome, curso e código."""

    def __init__(self, nome, id_aluno=-1, curso=None):
        """nome é um argumento obrigatório, os demais são opcionais (há valor␣↪→padrão)"""
        self.nome = nome
        self.id = id_aluno
        self.curso = curso
        
    def __str__(self):
        return "Aluno (" + self.nome + ": " + str(self.id) + ")"
        
# criando um objeto do tipo aluno
aluno = Aluno("Pedro")
print(aluno)
```
Aluno (Pedro: -1)

##  Adicionando métodos

Podemos adicionar métodos, que são funções que representam operações sobre um objeto de uma classe. Essas operações podem calcular e/ou retornar informações sobre o objeto ou ainda modificar os dados do objeto.

```python
class Aluno:
    """Esta classe representa um aluno,possui nome, curso e código."""
    
    def __init__(self, nome, id_aluno=-1, curso=None):
        """nome é um argumento obrigatório, os demais são opcionais (há valor␣↪→padrão)"""
        self.nome = nome
        self.id = id_aluno
        self.curso = curso
        
    def matricular(self, curso):
        if curso is not None:
            self.curso = curso
            return True
        return False
            
    def esta_matriculado(self):
        return self.curso is not None
        
    def esta_matriculado_em_curso(self, curso):
        return self.curso == curso
```

O método **__init__**, como visto anteriormente, é o inicializador da classe.  Quando criamos um objeto  da  classe Aluno,  é  esse  método  que  será  executado.   O  método  matricular  recebe  como parâmetro um curso e insere esse valor no atributo curso.  O método **esta_matriculado** verifica ovalor do atributo curso e retorna **True** se o valor for diferente de **None**. Observe a utilização do is not, apresentado anteriormente. Por fim, o método **esta_matriculado_em_curso** recebe um valor de um curso como parâmetro, compara com o valor do objeto e retorna True se o valor for igual.

Observe que os métodos recebem self que é como chamamos o objeto.

##  Utilizando métodos

Observe o exemplo abaixo.

```python
curso = "Ciência de Dados"
aluno = Aluno("João", 1)
print(aluno.esta_matriculado())
aluno.matricular(curso)
print(aluno.esta_matriculado())
print(aluno.esta_matriculado_em_curso(curso))
print(aluno.esta_matriculado_em_curso("Engenharia de Software"))
```
False

True

True

False

Na primeira linha,  a variável curso recebe o valor “Ciência de dados”. A segunda linha faz a instanciação de um objeto chamado aluno da classe Aluno, passando o valor “João” como nome eo valor 1 como id_aluno. Como nenhum valor foi passado para o curso, ao criar o objeto, o método __init__ irá atribuir o valor None para esse atributo.  A terceira linha faz uma chama ao método esta_matriculado().  Observe a forma como isso é feito.  Primeiro colocamos o nome do objeto, seguido de um ponto (.) e depois o nome do método. Como esse método não recebe parâmetros, não há valor entre os parênteses (mas é necessário colocar os parênteses). Como o valor que oobjeto  possui  no  atributo  curso  é None,  o  valor  da  operação self.curso  is  not  None retornará False. Na quarta linha, temos a atribuição da variável curso ao objeto aluno por meio do método matricular. Isso fará o valor do atributo curso do objeto aluno receber o valor “Ciência de dados”.

Ao realizar novamente a chamada do método esta_matriculado na linha 5, temos como resultado True,  pois o valor do atributo curso do objeto aluno não é mais None.   A sexta linha possui achamada para o método esta_matriculado_em_curso, passando como parâmetro a variável curso.

Como esse valor é igual ao valor do atributo curso do objeto aluno, o resultado retorna True. Por fim,  a  última  linha  faz  uma  outra  chamada  ao  método esta_matriculado_em_curso,  passandocomo parâmetro um outro curso.  Como o valor dos cursos é diferente, o resultado retornado é False.

##  del

Podemos remover um objeto comdelaluno = Aluno("João")

del aluno

Porém, o Python conta com coletor de lixo, e, se o programa estiver bem estruturado, é raro necessitar fazer a remoção de um objeto.

##  Métodos e Atributos da classe

Os  métodos  vistos  até  agora  são  métodos  que  atuam  sobre  o  objetoself,  porém  podemos  termétodos que atuam sobre a classe em si. Para isso, utilizamos o decorador @classmethod.

Métodos da classe são úteis para implementar funcionalidades como construtores específicos oumanter uma contagem de objetos instanciados. Veja que no exemplo abaixo implementamos dois métodos da classe. Algumas informações sobre a classe
 - inc_inst() é incrementado toda vez que uma classe é criada (e é chamado por__init()__)
 - novo_auto_id() é um construtor que usa o valor mantido porinc_inst()para automatica-mente atribuir um id incremental na construção
 - inst_count é um atributo da classe que armazena a quantidade de instancias da classe (quan-tos  objetos  já  foram  criados).    O  valor  é  atualizado  pela  chamada  ao  método  da  classe inc_inst() que é feito dentro do método __init()__.

```python
class Aluno:
    inst_count = 0
    
    @classmethod
    def inc_inst(cls):
        cls.inst_count += 1
    
    def __init__(self, nome, id_aluno=-1, curso=None):
        """nome é um argumento obrigatório, os demais são opcionais (há valor␣↪→padrão)"""
        Aluno.inc_inst() # chamada de método da classe
        self.nome = nome
        self.id = id_aluno
        self.curso = curso
    
    def __str__(self):
        return "Aluno (" + self.nome + ": " + str(self.id) + ")"
        
    @classmethod
    def novo_auto_id(cls, nome, *args, **kwargs):
        return cls(nome, cls.inst_count + 1, *args, **kwargs)
        
a1 = Aluno.novo_auto_id("João", curso="Eng. Software")
a2 = Aluno.novo_auto_id("Maria", curso="Ciência de Dados")
print(Aluno.inst_count)
print(a1)
print(a2)
print(Aluno.inst_count)
```

2

Aluno (João: 1)

Aluno (Maria: 2)

2

Observe que nos métodos de classe, utilizamos a palavra cls para nos referirmos à classe, assim como fazemos com self quando nos referimos ao objeto. No exemplo, com queremos fazer acesso à variável inst_count que é de escopo global da classe, usamos: 
cls.inst_count

Observe também como a função da classe é chamada no método construtor:

Aluno.inst_count()

Outro  ponto  a  ser  observado  é  a  utilização  de  um  novo  método  construtor  para  instanciar  osobjetos.  Isso ocorre nos objetos a1 e a2 instanciados no exemplo acima.  Também observe como podemos acessar o valor da variáve linst_countda classe Aluno (Aluno.inst_count).

## Métodos Estáticos

Métodos estáticos não recebem um objeto (self) nem uma classe (cls) como argumentos. Ou seja, não estão associados nem a classe nem a sua instância (objeto). Eles são como uma função normal, mas definidos dentro do namespace de uma classe.  É uma forma de conveniência para o agrupamento de funções relacionadas

```python
class Pessoa:
    @staticmethod
    def funcao_estatica_qualquer():
        print("Uma função estática na classe Pessoa")
        
Pessoa.funcao_estatica_qualquer()
```

Uma função estática na classe Pessoa

Observe que nos métodos relacionados a objetos (normais) chamamos o primeiro argumento do método (o objeto em si) de self e em métodos da classe (@classmethod), chamamos o primeiro argumento de cls(a classe). Esses nomes são apenas convenções, o desenvolvedor pode escolhero nome que achar mais conveniente. Porém o recomendado é manter a convenção.

# Herança

A herança permite que uma classe herde atributos e métodos de outras classes.  A grande vantagem do uso de herança é a reutilização de código entre classes.

A classe
Pessoa possui três atributos (nome,cpf e idade) e um método (aniversario). A classe Aluno possui um atributo (curso) e um método(matricular). Porém, a classe Aluno herda os atributos e métodos da classe Pessoa.

Sua implementação em Python fica:

```python
class Pessoa:
    
    def __init__(self, nome, cpf, idade=0):
        self.nome = nome
        self.cpf = cpf
        self.idade = idade
    
    def aniversario(self):
        self.idade += 1
    
    def texto(self):
        return self.nome + " (" + str(self.cpf) + ", "  + str(self.idade) + ")"
    
    def __str__(self):
        return self.texto()

class MixinNomes:
    
    def nome_minusculo(self):
        return self.nome.lower()
        
class Professor(Pessoa, MixinNomes):
    
    def __init__(self, nome, cpf, horas, departamento, *args, **kwargs):
        super().__init__(nome, cpf, *args, **kwargs) # Pessoa.__init__(self,␣↪→nome, cpf, *args, **kwargs)
        self.horas = horas
        self.departamento = departamento
        
    def mudar_horas(self, horas):
        self.horas = horas
        
    def texto(self):
        return "Professor: " + super().texto()
        
class Aluno(Pessoa):
    
    def __init__(self, nome, cpf, curso=None, *args, **kwargs):
        super().__init__(nome, cpf, *args, **kwargs)# Pessoa.__init__(self,␣↪→nome, cpf, *args, **kwargs)
        self.curso = curso
    
    def matricular(self, curso):
        self.curso = curso
        
    def texto(self):
        return "Aluno: " + super().texto()
    
a = Aluno("João", 18902929290, idade=20)
print(a)
p = Professor("Paulo", 12312312399, idade=30, horas=40, departamento="COENS")
print(p)
```

Aluno: João (18902929290, 20)
Professor: Paulo (12312312399, 30)

Observe nas linhas:
class Professor(Pessoa, MixinNomes):
e
class Aluno(Pessoa):

Definimos que a classe Professor e Aluno herdam da classe Pessoa.  Por hora, vamos ignorar aoutra super classe de Professor chamada de MixinNomes.

Observe como usamos o inicializador da classe Pessoa no construtor da classeAluno. Utilizamos super para fazer referência a classe pai (classe da qual herdamos métodos e atributos). Para fazer autilização do construtor da classe Pessoa, usamos super().__init__ passando os argumentos como parâmetro.

##  Super classe e sub classe

Do  ponto  de  vista  de  uma  classe,  no  exemplo  abaixo  a  classe Professor,  adotamos  a  seguinte terminologia para denominar as classes relacionadas:
 - Super classe:  É um pai da classe em questão, no nosso caso a classePessoa.  Note que uma classe pode ter várias super classes (herança múltipla)
 - Sub classe:  Uma classe que herda da classe em questão (“uma classe filha”),  no exemplo abaixo as classes Efetivo  e Temporario Note que esta terminologia é sempre relacional, dizemos que Pessoa é uma super classe de Professor e que Professor é uma sub classe de Pessoa.
 
##  Sobrescrita de métodos

Uma classe pode sobrescrever os métodos de sua(s) super classe(s). Basta reimplementar o métodocom o mesmo nome. No código do exemplo anterior, isso ocorre com os métodos __init__ e texto das classes Professor e Aluno.

##  super()

O super retorna um objeto proxy(procurador/representante) para asuper classe do objeto atual, no caso da função __init__ da classe Professor é retornado um proxy para o objeto em questão como se ele fosse da classe Pessoa. Isso nos permite usar métodos da super classe na classe atual.

O super() é particularmente útil quando temos sobrescrita de métodos.   Observe nos métodos texto das classes Professor e Aluno como reaproveitamos o código do método de mesmo nomeda classe Pessoa. O mesmo reaproveitamento ocorre com o método__init__.

##  Mixins

Mixins são classes que providenciam funcionalidades que podem ser úteis para várias classes, mas não representam em si uma classe que será instanciável em um objeto. Eles agrupam funções úteis, modificam o comportamento da classe.  Sua principal vantagem é o reaproveitamento de código.

Em termos práticos, o Mixin é uma super classe que pode ser “misturada” em várias classes.

Observe como o método nome_minusculo definido no Mixin MixinNomes está disponível na classe Professor:

```python
p = Professor("Paulo", 12312312399, idade=30, horas=40, departamento="COENS")
print(p.nome_minusculo())
```
paulo

Observe que a classe Aluno não tem incorporada a ela o Mixin.  Há uma outra estratégia de seu tilizar Mixins que é criar uma classe especifica para adicionar o Mixin a uma classe base, veja a definição da classe AlunoComNomes:

```python
class AlunoComNomes(Aluno, MixinNomes):
    pass

a = AlunoComNomes("Alberto Junior da Silva", 12312334500, idade=21)
a.nome_minusculo()
```

A classe AlunoComNomes é uma nova classe Aluno com a adição das funcionalidades do Mixin MixinNomes.  Note o uso da palavra reservada pass.  O pass serve para indicar a ausência de instruções em uma função ou de funções e atributos em uma classe.  No nosso caso, indica que a classe AlunoComNomes é apenas formada pela junção das classes Aluno e MixinNomes e nada mais.

# Sobrecarga de operadores

A sobrecarga de operadores possibilita definir o comportamento dos objetos ao serem utilizados com os diversos operadores (e.g., lógicos, relacionais).

##  conversão de tipos:

O  Python  suporta  os  seguintes  operadores  para  a  conversão  de  tipos,  já  vimos__str__para  aconversão com str():
 - __str__(self): para string, str()
 - __int__(self): para inteiros, int()
 - __float__(self): para números de ponto flutuante, float()
 - __bool__(self): para valores lógicos booleanos, bool()

##  operadores aritméticos:

Classes em Python suportam a sobrecarga de operadores. Para isto deve-se implementar funções com nomes específicos:
 - __add(self, obj2)__: Adição (obj1 + obj2)
 - __sub(self, obj2)__: Subtração (obj1 - obj2)
 - __mul(self, obj2)__: Multiplicação (obj1 * obj2)
 - __pow(self, obj2)__: Exponenciação (obj1 ** obj2)
 - __truediv(self, obj2)__: Divisão (obj1 / obj2)
 - __floordiv(self, obj2)__: Divisão de ponto flutuante (obj1 // obj2)
 - __mod(self, obj2)__: Módulo (obj1 % obj2)
 - __lshift(self, obj2)__: Deslocamento para a esquerda (obj1 « obj2)
 - __rshift(self, obj2)__: Deslocamento para a direita (obj1 » obj2)

## Operadores de comparação

Os operadores de comparação são:
 - __eq(self, obj2)__: Igualdade (obj1 == obj2)
 - __ne(self, obj2)__: Desigualdade (obj1 != obj2)
 - __lt(self, obj2)__: Menor que (obj1 < obj2)
 - __gt(self, obj2)__: Maior que (obj1 > obj2)
 - __le(self, obj2)__: Menor ou igual que (obj1 <= obj2)
 - __ge(self, obj2)__: Maior ou igual que (obj1 >= obj2)

Estas funções devem retornar True ou False.

## Exemplo

Observe a classe abaixo que implementa um objeto de número racional (i.e. um numerador e umdenominador inteiro).  Nesse exemplo, temos o método __add__ responsável por realizar a somados números racionais (frações).

```python
class Racional:
    
    def __init__(self, num=0, den=1):
        self._num = int(num)
        self._den = int(den)
    
    def __str__(self):
        """Converte para string, chamado com str(objeto)"""
        return str(self._num) +'/'+ str(self._den)
        
    def __int__(self):
        """Converte para inteiro, chamado com int(objeto)"""
        return int(self._num / self._den)
        
    def __float__(self):
        """Converte para float, chamado com float(objeto)"""
        return self._num / self._den

    def __add__(self, obj2):
        if isinstance(obj2, int) or isinstance(obj2, float):
            obj2 = Racional(obj2, 1)
            num = self._num * obj2._den + self._den * obj2._num
            den = self._den * obj2._den
            return Racional(num, den)
            
    def __eq__(self, obj2):
        return float(self) == float(obj2)
        
    def __ne__(self, obj2):
        return float(self) != float(obj2)
        
    def __lt__(self, obj2):
        return float(self) < float(obj2)
        
    def __gt__(self, obj2):
        return float(self) > float(obj2)
        
    def __le__(self, obj2):
        return float(self) <= float(obj2)
        
    def __ge__(self, obj2):
        return float(self) >= float(obj2)

x = Racional(3,2)
print("Valor de x:", x)
y = Racional(4,5)
print("Valor de y:", y)
z = x + y
print("Valor de z:", z)
print(float(z))
```

Valor de x: 3/2

Valor de y: 4/5

Valor de z: 23/10

2.3

Vamos ver com mais detalhes a função __add__.  Como estamos trabalhando com sobrecarga de operadores, toda vez que houver uma soma do objeto da classe Racional como primeiro termo,essa função será executada de forma a realizar essa soma.  Isso ocorre no nosso exemplo quando executamos a linha z = x + y.  Ao executarmos essa linha, a função __add__ é executada, recebendo como parâmetro x como self e como obj2.  Após isso, há um if para verificar se o obj2 é um inteiro ou um float.  Essa validação é feita pois caso o obj2 não seja uma fração, será necessário transformá-lo em uma fração. Isso é feito adicionando o valor de 1 no denominador. Por exemplo, se quiséssemos somar 3/2 + 2, teríamos que transformar o 2 em número racional deixando-o na forma 2/1. Isso é feito com a linha:

obj2 = Racional(obj2, 1).

Após isso, é feito a soma dos dois valores racionais.  Primeiro, calculamos o valor do numerador salvo na variável num e depois calculamos o valor do denominador, salvo na variável (den). Por fim, o resultado desse método é um objeto da classe Racional com o numerador e denominador calculados. 

Abaixo testamos as comparações. Observe que a nossa estratégia de implementação foi converteros números racionais em float, que chama o método de conversão __float__ e usar a comparação padrão entre números de ponto flutuante (float).

```python
print("x == y", x == y)
print("x != y", x != y)
print("x < y", x < y)
print("x > y", x > y)
print("y < x", y < x)
```

x == y False

x != y True

x < y False

x > y True

y < x True
    

# Bibliografia

John Hunt. **A Beginners Guide to Python 3 Programming.**  Undergraduate Topics in ComputerScience. Springer, 2019.

Kent D. Lee. **Python Programming Fundamentals.**  Undergraduate Topics in Computer Science.Springer, 2014.