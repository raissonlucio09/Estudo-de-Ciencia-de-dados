# Python: Operadores aritméticos, relacionais e lógicos

Uma variável reserva espaço de memória para armazenar um dado e é referenciada por um nome. Python trabalha com três tipos básicos (numérico, string e booleano) e usa operadores aritméticos, relacionais e lógicos para calcular e comparar valores.

 Conceitos
- Tipos de dados: numérico (`int` sem casas decimais e `float` com casas decimais), texto (`str`) e booleano (`bool`, só `True` ou `False`)
- `print()` exibe mensagens; `input()` lê dados do teclado (o valor lido vem como texto)
- Operadores aritméticos: unários (`+` e `-` de sinal) e binários (`*`, `/`, `%`, `+`, `-`); parênteses mudam a prioridade
- Operadores relacionais: `==`, `>`, `<`, `>=`, `<=`, `!=` (sempre retornam `True` ou `False`)
- Operadores lógicos: `not`, `and`, `or` (prioridade: `not`, depois `and`, depois `or`)

 Exemplos e lugares aplicados
Cálculos em geral, validação de dados digitados pelo usuário e decisões que dependem de mais de uma condição.

Minhas anotações da aula
Uma variável reserva espaço de memória para armazenar um certo tipo de dado e relacionado a um nome para referenciar o seu conteúdo (nome da variável). Uma variável é um espaço de memória que pode conter, a cada tempo, valores diferentes.

Python trabalha com 3 tipos de dados básicos: numérico, string e booleano. Nos numéricos temos o tipo inteiro, que não possui casa decimal, e o número real - ponto flutuante (float), que possui casas decimais.

- Função `print()`: exibe mensagens. Para juntar textos e variáveis pode-se usar `+` (só entre strings; entre string e número dá erro) ou a vírgula.
- Função `input()`: lê dados do teclado.
- Operadores aritméticos, por prioridade: sinal `+`/`-` (unário), depois `*`, `/`, `%` (resto da divisão) e por último `+` e `-` (binários).
- Operadores relacionais têm todos o mesmo nível de prioridade. Em Python 3 o "diferente" é `!=` (o `<>` não existe mais).
- Operadores lógicos: NOT (negação), AND (conjunção, "E") e OR (disjunção, "OU").
- No exemplo de operadores: `k = z+w/x` dá 502.0 porque a divisão tem prioridade sobre a soma (200/100 = 2, depois 500 + 2). `z>w and w>y` é falso porque as duas condições precisam ser verdadeiras; `z>w or w>y` é verdadeiro porque basta uma.

## Código

### Tipos de dados
```python
x = "UNINOVE"
a = 10
b = 8.6
c = False
print(type(x))
print(type(a))
print(type(b))
print(type(c))
```
Saída:
```
<class 'str'>
<class 'int'>
<class 'float'>
<class 'bool'>
```

### Função print
```python
x = "UNINOVE"
y = "LEONARDO"
a = 10
print("Bem vindo ao mundo Python")
print(a)
print(y)
print(x)
```
Saída:
```
Bem vindo ao mundo Python
10
LEONARDO
UNINOVE
```

### Concatenação
```python
x = "UNINOVE"
y = "LEONARDO"
a = 10
print("Bem vindo ao mundo Python com "+y + " professor da " + x, "que é", a)
```
Saída:
```
Bem vindo ao mundo Python com LEONARDO professor da UNINOVE que é 10
```

### Leitura de dados do teclado
```python
print("dados do aluno")
nome = input("informe seu nome: ")
idade = input("informe sua idade: ")
print(nome, "você tem", idade, "anos!!")
```
Saída:
```
dados do aluno
informe seu nome: Leonardo
informe sua idade: 42
Leonardo você tem 42 anos!!
```

### Operadores aritméticos, relacionais e lógicos
```python
x = 100
y = 300
z = 500
w = 200

k = x+y+z
print(k)
k = z+w/x
print(k)
print(z>w)
print(w>z)
print(y+w==z)
print(z>w and w>y)
print(z>w or w>y)
print(not y+w==z)
```
Saída:
```
900
502.0
True
False
True
False
True
False
```
