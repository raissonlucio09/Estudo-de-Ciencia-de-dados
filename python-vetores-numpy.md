# Python: Vetores (NumPy)

Vetores são matrizes de uma só dimensão. A biblioteca NumPy faz cálculos matemáticos de forma simples e rápida, e é muito usada em aprendizado de máquina e processamento de imagens, pois trabalha com vetores e matrizes.

## Conceitos
- `np.array()` cria vetores e matrizes
- Atributos: `shape` (formato), `dtype` (tipo dos valores), `size` (quantidade de elementos), `itemsize` (bytes de cada elemento) e `ndim` (número de dimensões)
- Acesso e alteração pelo índice, que começa em 0
- Criação de vetores prontos: `empty`, `zeros`, `ones`, `arange` e `random.random`
- `arange(inicio, parada, passo)`: o valor de parada não entra

## Exemplos e lugares aplicados
Cálculos numéricos, aprendizado de máquina, imagens (que são matrizes de pixels) e geração de números aleatórios.

## Minhas anotações da aula
- Vetor = matriz unidimensional (uma única coluna).
- `shape (4,)` indica 4 elementos; `dtype int32` indica inteiros de 32 bits (4 bytes); `size` é 4 (quantidade de elementos) e `itemsize` é 4 (bytes por elemento). Com decimais o tipo vira `float64` (8 bytes por elemento).
- `empty` cria o vetor com valores quaisquer (lixo de memória); o ideal é iniciar com `zeros` ou `ones`.
- No `arange(3,13,2,float)` os valores vão de 3 até antes de 13, de 2 em 2: 3, 5, 7, 9, 11.
- `6*np.random.random(5)` gera 5 valores aleatórios entre 0 e 6.

## Código

### Exemplo 1: criação e atributos
```python
import numpy as np

vetor = np.array([8, 34, 67, 98])
print(vetor)
print("Shape:",vetor.shape)
print("Dtype:",vetor.dtype)
print("Size:",vetor.size)
print("Itemsize:",vetor.itemsize)
print("Ndim:", vetor.ndim)

vetor = np.array([8.87, 34, 67.89, 98, 1.09])
print(vetor)
print("Shape:",vetor.shape)
print("Dtype:",vetor.dtype)
print("Size:",vetor.size)
print("Itemsize:",vetor.itemsize)
print("Ndim:", vetor.ndim)
```
Saída (o `int32` pode aparecer como `int64` dependendo do sistema):
```
[ 8 34 67 98]
Shape: (4,)
Dtype: int32
Size: 4
Itemsize: 4
Ndim: 1
[ 8.87 34.   67.89 98.    1.09]
Shape: (5,)
Dtype: float64
Size: 5
Itemsize: 8
Ndim: 1
```

### Exemplo 2: acessar e alterar
```python
import numpy as np

vetor = np.array([8, 34, 67, 98])
print("Vetor posicao 0:",vetor[0])
print("Vetor posicao 2:",vetor[2])
vetor[1] = 231
vetor[3] = 105
print(vetor)
```
Saída:
```
Vetor posicao 0: 8
Vetor posicao 2: 67
[  8 231  67 105]
```

### Exemplo 3: formas de criar vetores
```python
import numpy as np

vetor01 = np.empty(10,int)
print(vetor01)
vetor02 = np.zeros(10)
print(vetor02)
vetor03 = np.ones(10)
print(vetor03)
vetor04 = np.arange(3,13,2,float)
print(vetor04)
vetor05 = 6*np.random.random(5)
print(vetor05)
```
Saída (o `empty` e o `random` mudam a cada execução):
```
[ valores quaisquer ]
[0. 0. 0. 0. 0. 0. 0. 0. 0. 0.]
[1. 1. 1. 1. 1. 1. 1. 1. 1. 1.]
[ 3.  5.  7.  9. 11.]
[2.54885066 2.52142094 3.55445242 1.77394734 0.15435305]
```
