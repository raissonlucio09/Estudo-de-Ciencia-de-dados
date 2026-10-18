# Desvio condicional

Os desvios condicionais (estruturas de seleção ou decisão) verificam condições para decidir se uma instrução, ou uma sequência de instruções, será executada. Também servem para escolher entre opções.

## Conceitos
- Desvio condicional simples: `if` executa o bloco só se a condição for verdadeira
- Desvio condicional composto: `if ... else` tem um bloco para verdadeiro e outro para falso
- Desvio condicional encadeado: `if ... elif ... else` testa várias condições em sequência
- Em Python a indentação (espaços no início da linha) define o que pertence ao bloco do `if`
- Teste de mesa: executar o programa "no papel", passo a passo, anotando os valores das variáveis

## Exemplos e lugares aplicados
Validar se um valor digitado atende a uma regra, calcular algo diferente conforme a situação, menus de opções.

## Minhas anotações da aula
- `if (condição):` executa as linhas indentadas só se a condição for verdadeira; as linhas sem indentação logo depois rodam sempre.
- Exemplo 1 (a == b): o bloco roda, c vira 15 e d = 25. Exemplo 2 (a != b): o bloco não roda, c continua 2 e d = 12.
- Exemplo 3: a única mudança é a indentação da linha `c = c + 5`. Fora do `if`, ela roda sempre e o resultado passa a ser 17. Python é sensível à indentação.
- `if...else`: se a condição é verdadeira roda o primeiro bloco, senão roda o bloco do `else`. No exemplo 4, com b = 5 o resultado é 23 e com b = 2 o resultado é 15.
- `if...elif...else`: testa as condições na ordem e executa só o primeiro bloco verdadeiro; o `else` roda se todas forem falsas. No exemplo 5, digitar 1 a 5 imprime de 10 a 14 e qualquer outro valor imprime 20.

## Código

### Exemplo 1 (condição verdadeira)
```python
a=5
b=5
c=2
d=0
if (a==b):
    c = a+b
    c = c + 5
d = c + 10
print(d)
```
Saída: `25`

### Exemplo 2 (condição falsa)
```python
a=5
b=3
c=2
d=0
if (a==b):
    c = a+b
    c = c + 5
d = c + 10
print(d)
```
Saída: `12`

### Exemplo 3 (a indentação muda o resultado)
```python
a=5
b=3
c=2
d=0
if (a==b):
    c = a+b
c = c + 5
d = c + 10
print(d)
```
Saída: `17`

### Exemplo 4 (if...else)
```python
a=5
b=int(input("informe valor de b: "))

c=2
d=0
if (a==b):
    c = a+b
    c = c + 3
else:
    c = a-b
    c = c + 2
d = c +10
print(d)
```
Saída: `23` se b = 5 e `15` se b = 2

### Exemplo 5 (if...elif...else)
```python
c = 0
a=int(input("informe valor de a: "))
if (a==1):
    c = 10
elif (a==2):
    c = 11
elif (a==3):
    c = 12
elif (a==4):
    c = 13
elif (a==5):
    c = 14
else:
    c = 20
print(c)
```
Saída: de `10` a `14` para a de 1 a 5, e `20` para qualquer outro valor.
