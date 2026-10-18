# Python: Computação Científica com SciPy

SciPy é uma biblioteca de código aberto para computação científica de alta performance, feita para engenheiros, matemáticos, cientistas e estatísticos. Funciona junto com os arrays do NumPy. Nesta aula foi usada para álgebra linear.

## Conceitos
- Matriz inversa: só existe para matriz quadrada; A x A⁻¹ = I (matriz identidade, com 1 na diagonal e 0 no resto)
- `linalg.inv(A)` calcula a inversa
- Sistema de equações lineares: A·X = B, logo X = A⁻¹·B; também pode ser resolvido com `solve()`
- Determinante: definido para matrizes quadradas; calculado com `det()`
- `round(valor, casas)` arredonda para o número de casas decimais desejado

## Exemplos e lugares aplicados
Resolver sistemas de equações, otimização, integração numérica e cálculos de engenharia e estatística.

## Minhas anotações da aula
- A prova real da inversa é multiplicar A pela inversa e obter a matriz identidade.
- O sistema do exemplo (x + y + z = 6; 8x + 3y - z = 8; 2x - 3y + z = 12) tem solução x = 2, y = -1 e z = 5.
- `solve()` pode dar pequenas diferenças (como -0.9999999999999998) por arredondamento; usa-se `round()` para ajustar.
- Determinante de ordem 1 é o próprio valor; de ordem 2 é (a·d) - (b·c); de ordem 3 usa a regra de Sarrus (replicar as duas primeiras colunas à direita).

## Código

### Exemplo 1: matriz inversa
```python
import numpy as np
from scipy import linalg

A = np.array([[3, 0, 2],[9, 1, 7],[1, 0, 1]])
Ainversa = linalg.inv(A)
print("Matriz A")
print(A)
print("Matriz A inversa")
print(Ainversa)
```
Saída da inversa:
```
[[ 1.  0. -2.]
 [-2.  1. -3.]
 [-1.  0.  3.]]
```

### Exemplo 2: prova real
```python
import numpy as np
from scipy import linalg

A = np.array([[3, 0, 2],[9, 1, 7],[1, 0, 1]])
Ainversa = linalg.inv(A)
B = A.dot(Ainversa)
print(B)
```
Saída (matriz identidade):
```
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

### Exemplo 3: sistema de equações com a inversa
```python
import numpy as np
from scipy import linalg

A = np.array([[1, 1, 1],[8, 3, -1],[2, -3, 1]])
B = np.array([[6],[8],[12]])
Ainversa = linalg.inv(A)
C = Ainversa.dot(B)
print(C)
print("Valor da variável x:", C[0][0])
print("Valor da variável y:", C[1][0])
print("Valor da variável z:", C[2][0])
```
Saída: `x = 2.0`, `y = -1.0`, `z = 5.0`

### Exemplos 4 e 5: função solve e round
```python
import numpy as np
from scipy import linalg

A = np.array([[1, 1, 1],[8, 3, -1],[2, -3, 1]])
B = np.array([[6],[8],[12]])
C = np.linalg.solve(A, B)
print(C)
print("Valor da variável x:", round(C[0][0],2))
print("Valor da variável y:", round(C[1][0],2))
print("Valor da variável z:", round(C[2][0],2))
```
Saída: `x = 2.0`, `y = -1.0`, `z = 5.0` (sem o `round`, o y sai como -0.9999999999999998).

### Exemplo 6: determinante
```python
import numpy as np
from scipy import linalg

A = np.array([[8]])
B = np.array([[4,2],[3,3]])
C = np.array([[1,4,2],[1,3,3],[2,6,1]])

print("Determinante de A")
print(round(np.linalg.det(A),2))
print("Determinante de B")
print(round(np.linalg.det(B),2))
print("Determinante de C")
print(round(np.linalg.det(C),2))
```
Saída: `8.0`, `6.0` e `5.0`
