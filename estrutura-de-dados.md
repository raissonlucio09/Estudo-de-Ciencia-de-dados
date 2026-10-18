# Estrutura de dados

Estruturas de dados guardam vários valores em uma única variável. Em Python as principais são lista, tupla, dicionário e conjunto.

## Conceitos
- Lista `[ ]`: ordenada e pode ser alterada; acessa-se pelo índice (começa em 0)
- Tupla `( )`: ordenada, mas não pode ser alterada depois de criada
- Dicionário `{chave: valor}`: guarda pares chave/valor
- Conjunto `{ }`: não guarda valores repetidos e não tem ordem
- Funções úteis: `len()`, `append()`, `sorted()`, `in`

## Exemplos e lugares aplicados
Lista de notas de alunos, cadastro de uma pessoa (dicionário), remover duplicados de uma lista (conjunto).

## Minhas anotações da aula
(Escreva aqui com suas palavras o que o professor explicou nesta aula.)

## Código
```python
# Lista
frutas = ["maçã", "banana", "uva"]
frutas.append("laranja")
print(frutas[0], len(frutas))   # maçã 4

# Tupla
coordenada = (10, 20)
print(coordenada[1])            # 20

# Dicionário
aluno = {"nome": "Ana", "idade": 20}
aluno["curso"] = "ADS"
print(aluno["nome"])            # Ana

# Conjunto
numeros = {1, 2, 2, 3, 3}
print(numeros)                  # {1, 2, 3}
```
