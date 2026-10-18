# Métodos e funções

Uma função é um bloco de código com nome que pode ser chamado várias vezes, recebendo valores (parâmetros) e podendo devolver um resultado. Métodos são funções que pertencem a um objeto, como `texto.upper()`.

## Conceitos
- Criação com `def nome(parametros):`
- `return` devolve um valor para quem chamou a função
- Parâmetros podem ter valor padrão
- Funções prontas: `print`, `len`, `type`, `round`, `input`
- Métodos: `"texto".upper()`, `lista.append(x)`

## Exemplos e lugares aplicados
Evitar repetir código, organizar o programa em partes e reaproveitar cálculos.

## Minhas anotações da aula
(Escreva aqui com suas palavras o que o professor explicou nesta aula.)

## Código
```python
def soma(a, b):
    return a + b

print(soma(3, 4))        # 7

def saudacao(nome="aluno"):
    print("Olá,", nome)

saudacao()               # Olá, aluno
saudacao("Leonardo")     # Olá, Leonardo

# Métodos de string
print("uninove".upper()) # UNINOVE
print(round(3.14159, 2)) # 3.14
```
