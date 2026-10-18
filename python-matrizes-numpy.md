# Python: Matrizes (NumPy)

Matrizes são arrays com mais de uma dimensão (o mais comum é linhas e colunas). Com o NumPy é fácil criar, alterar e fazer operações matemáticas com matrizes.

 Conceitos
- `np.array([[...],[...]])` cria uma matriz; `matriz[linha][coluna]` acessa um elemento (índices começam em 0)
- Soma e subtração com `+` e `-`; multiplicação de matrizes com `dot()`
- Na multiplicação C = A x B, as colunas de A devem ser iguais às linhas de B; C tem as linhas de A e as colunas de B
- `concatenate()` junta matrizes e `split()` divide (as partes precisam ter o mesmo número de linhas)
- Matriz transposta (troca linhas por colunas): `transpose()`
- Funções estatísticas: `sum`, `min`, `max`, `ptp`, `mean`, `var` (variância) e `std` (desvio padrão)
- `reshape` não altera a original e precisa manter a quantidade de elementos; `resize` altera a original e pode mudar a quantidade (completa com 0)

Exemplos e lugares aplicados
Álgebra linear, processamento de imagens, aprendizado de máquina e estatística.

Minhas anotações da aula
- A matriz do exemplo 1 tem 4 linhas e 3 colunas; o elemento (1,2) é o 6 (segunda linha, terceiro elemento).
- Produto 4x3 por 3x2 resulta em matriz 4x2.
- `split(matriz, 2)` divide em 2 partes iguais; dividir em 3 dá erro porque 4 linhas não se dividem igualmente, mas em 4 partes funciona.
- `reshape(8,2)` de uma matriz com 15 elementos dá `ValueError`; já o `resize(8,2)` funciona e acrescenta um 0 no final.

## Código

### criar e alterar
```python
import numpy as np

matriz = np.array([[1,2,3],[4,5,6],[7,8,9],[10,20,30]])
print("Matriz:",matriz)
print("Elemento posicao (1,2):",matriz[1][2])
print("Dimensoes:",matriz.ndim)
matriz[3][1] = 18
print("Matriz:",matriz)
```
Saída: o elemento (1,2) é `6`, as dimensões são `2` e depois da alteração a última linha vira `[10 18 30]`.

### soma, subtração e produto
```python
import numpy as np

matriz01 = np.array([[1,2,3],[4,5,6],[7,8,9],[10,20,30]])
matriz02 = np.array([[2,2,2], [6,9,-10], [1,7,9], [3,6,8]])
matriz03 = np.array([[1,1], [0,4], [2,2]])

matrizsoma = matriz01 + matriz02
matrizsub = matriz01 - matriz02
matrizprod = matriz01.dot(matriz03)

print("Soma Matriz 01 + Matriz 02")
print(matrizsoma)
print("Subtracao Matriz 01 - Matriz 02")
print(matrizsub)
print("Produto Matriz 01 x Matriz 03")
print(matrizprod)
```
Saída:
```
[[ 3  4  5]
 [10 14 -4]
 [ 8 15 18]
 [13 26 38]]
[[-1  0  1]
 [-2 -4 16]
 [ 6  1  0]
 [ 7 14 22]]
[[  7  15]
 [ 16  36]
 [ 25  57]
 [ 70 150]]
```

###  concatenar
```python
import numpy as np

matriz01 = np.array([[1,2,3],[4,5,6],[7,8,9],[10,20,30]])
matriz02 = np.array([[2,2,2], [6,9,-10], [1,7,9], [3,6,8]])
matriz03 = np.zeros((1,3))
matrizresultante = np.concatenate((matriz01,matriz02,matriz03))
print(matrizresultante)
```
Saída: uma matriz de 9 linhas e 3 colunas (as 4 linhas da primeira, as 4 da segunda e a linha de zeros).

### dividir
```python
import numpy as np

matriz01 = np.array([[1,2,3],[4,5,6],[7,8,9],[10,20,30]])
matrizresultante = np.split(matriz01,2)
print(matrizresultante[0])
print(matrizresultante[1])
```
Saída:
```
[[1 2 3]
 [4 5 6]]
[[ 7  8  9]
 [10 20 30]]
```

### transposta
```python
import numpy as np

matriz = np.array([[10, 20],[30,40],[50,60],[70,80]])
matrizt = matriz.transpose()
print(matriz)
print(matrizt)
```
Saída da transposta:
```
[[10 30 50 70]
 [20 40 60 80]]
```

### funções estatísticas
```python
import numpy as np

matriz = np.array([[1,2,3],[4,5,6],[7,8,9],[10,20,33]])
print("Max:",matriz.max())
print("Min:",matriz.min())
print("Ptp:",matriz.ptp())
print("Sum:",matriz.sum())
print("Mean:",matriz.mean())
print("Var:",matriz.var())
print("Std:",matriz.std())
```
Saída:
```
Max: 33
Min: 1
Ptp: 32
Sum: 108
Mean: 9.0
Var: 75.16666666666667
Std: 8.669871202426636
```
Observação: em versões novas do NumPy (2.0 ou mais) o `matriz.ptp()` foi removido; use `np.ptp(matriz)`.

### reshape e resize
```python
import numpy as np

matriz = np.array([[1,2,3,4,5],[6,7,8,9,10],[11,12,13,14,15]])
print("Reshape")
print(matriz.reshape(5,3))
print("matriz após reshape")
print(matriz)
print("Efetuar resize")
matriz.resize(8,2)
print("Matriz após resize")
print(matriz)
```
Saída: o `reshape(5,3)` mostra a matriz reorganizada, mas a original continua 3x5. Depois do `resize(8,2)` a matriz fica com 8 linhas e 2 colunas, e o último elemento é `0`.
