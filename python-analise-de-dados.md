# Python: Análise de Dados

Uma forma de predizer um valor a partir de valores conhecidos é a regressão linear. Em Python ela pode ser feita com o pacote NumPy (`polyfit`, para polinômios) e com a biblioteca scikit-learn (regressão linear múltipla).

## Conceitos
- `np.polyfit(x, y, grau)` ajusta um polinômio aos pontos; `np.poly1d()` monta a função
- Grau 1: `Y = aX + b`; grau 2: `Y = aX² + bX + c`; grau 3 e assim por diante
- Resíduo: diferença entre os pontos observados e a curva obtida (`full=True` no `polyfit`)
- Regressão linear múltipla com `LinearRegression` do scikit-learn: `Y = aX + bZ + cW + d`
- Erro médio quadrado: média das diferenças ao quadrado entre o predito e o real

## Exemplos e lugares aplicados
Prever vendas, preços e demanda a partir de variáveis conhecidas.

## Minhas anotações da aula
- No exemplo 1 os pontos (1,5), (2,8), (3,11) e (4,14) geram `Y = 3X + 2`; prevendo X = 10, o resultado é 32.
- No exemplo 3, os polinômios de grau 1, 2 e 3 foram comparados: o grau 3 teve resíduo 0, o grau 2 teve resíduo bem menor que o grau 1, e a previsão para X = 25 foi parecida entre os graus 2 e 3 e bem distante no grau 1.
- No exemplo 4 os dados foram gerados com `Y = 3X - 2Z + W - 2` e a regressão recuperou exatamente essa função (erro 0). Na prática a função é desconhecida e a regressão tenta descobri-la.

## Código

### Exemplo 1: polinômio de grau 1
```python
import numpy as np
import matplotlib.pyplot as plt

x = [1,2,3,4]
y = [5,8,11,14]
fit = np.polyfit(x,y,1)
fit_fn = np.poly1d(fit)
print("Y = aX + b. Então a =",round(fit[0],2), "e b =",round(fit[1],2))
print(fit_fn)
print(round(fit_fn(10),4))
plt.plot(x,y, 'bo', x, fit_fn(x), 'red')
plt.xlim(0, 5)
plt.ylim(0, 15)
plt.show()
```
Saída:
```
Y = aX + b. Então a = 3.0 e b = 2.0

3 x + 2
32.0
```

### Exemplo 2: polinômio de grau 2
```python
import numpy as np
import matplotlib.pyplot as plt

x = [0,1,2,3,4,5,6,7]
y = [-1,4.01,13,26,43.01,64.02,88.98,118]
fit = np.polyfit(x,y,2)
fit_fn = np.poly1d(fit)
print(fit)
print(fit_fn)
print(round(fit_fn(10),4))
plt.plot(x,y, 'o', x, fit_fn(x), 'red')
plt.show()
```
Saída:
```
[ 1.99928571  3.00404762 -0.99916667]
1.999 x² + 3.004 x - 0.9992
228.9699
```

### Exemplo 3: comparando graus 1, 2 e 3 (com resíduo)
```python
import numpy as np
import matplotlib.pyplot as plt

x = [0,5,10,20,30,40,50]
y = [1,59.75,356,2411,7666,17621,33776]

# grau 1
fit = np.polyfit(x,y,1,full=True)
fit_fn1 = np.poly1d(fit[0])
residuo1 = fit[1][0]
# grau 2
fit = np.polyfit(x,y,2,full=True)
fit_fn2 = np.poly1d(fit[0])
residuo2 = fit[1][0]
# grau 3
fit = np.polyfit(x,y,3,full=True)
fit_fn3 = np.poly1d(fit[0])
residuo3 = fit[1][0]

print("Polinomio Grau 1. Resíduo:",round(residuo1,2), "Predição para valor igual a 25: ",round(fit_fn1(25),4))
print("Polinomio Grau 2. Resíduo:",round(residuo2,2), "Predição para valor igual a 25: ",round(fit_fn2(25),4))
print("Polinomio Grau 3. Resíduo:",round(residuo3,2), "Predição para valor igual a 25: ",round(fit_fn3(25),4))

plt.plot(x,y, 'o', x, fit_fn1(x), 'brown')
plt.plot(x,y, 'o', x, fit_fn2(x), 'red')
plt.plot(x,y, 'o', x, fit_fn3(x), 'blue')
plt.show()
```
Saída:
```
Polinomio Grau 1. Resíduo: 154762073.65 Predição para valor igual a 25:  10623.4616
Polinomio Grau 2. Resíduo: 4243194.09 Predição para valor igual a 25:  4574.9366
Polinomio Grau 3. Resíduo: 0.0 Predição para valor igual a 25:  4544.75
```
Gráfico: grau 1 em marrom, grau 2 em vermelho e grau 3 em azul.

### Exemplo 4: regressão linear múltipla (scikit-learn)
```python
import numpy as np
from sklearn import linear_model

x_train = np.array([[1,1,1],[2,3,5],[3,4,4],[4,6,7],[7,8,9],[5,2,1],[3,4,5],[3,3,3],[4,4,4],[5,5,5]])
y_train = np.array([0,3,3,5,12,10,4,4,6,8])

model = linear_model.LinearRegression().fit(x_train, y_train)
print("Y = " + str(round(model.coef_[0],2))+"X + " + str(round(model.coef_[1],2)) + "Z + " + str(round(model.coef_[2],2)) + "W + "+ str(round(model.intercept_,2)))
print("Erro médio quadrado: %.2f" % np.mean((model.predict(x_train) - y_train) ** 2))
print(model.predict([[10,10,10]]))
```
Saída:
```
Y = 3.0X + -2.0Z + 1.0W + -2.0
Erro médio quadrado: 0.00
[18.]
```
