# Visualização de resultados com Matplotlib

O Matplotlib é uma biblioteca livre e de código aberto para gráficos 2D em Python. O módulo `pyplot` tem uma interface parecida com a do MATLAB (que é pago e focado em cálculo numérico).

 Conceitos
- `plt.plot(x, y)` desenha linhas ou pontos; sem o eixo X, os pontos usam 0, 1, 2...
- Formato do gráfico em texto: cor + marcador/linha. Cores: `r` vermelho, `g` verde, `b` azul, `m` magenta, `k` preto. Marcadores: `o` ponto, `D` losango. Linhas: `--` tracejada
- `plt.xlabel()`, `plt.ylabel()` e `plt.title()` dão nomes aos eixos e ao gráfico
- `plt.xlim()` e `plt.ylim()` limitam os eixos
- Histograma (`plt.hist`), pizza (`plt.pie`) e barras (`plt.bar` e `plt.barh`)
- `plt.legend()` mostra a legenda e `plt.show()` exibe o gráfico

Exemplos e lugares aplicados
Relatórios, pesquisas eleitorais, distribuição de frequências, comparação de grupos e apresentação de resultados de análise de dados.

Minhas anotações da aula
- No exemplo 3, o parâmetro `'ro'` significa vermelho (r) e pontos (o) em vez da reta padrão.
- No exemplo 6, é possível desenhar reta e pontos no mesmo `plot`, e o título vem do `plt.title()`.
- Histograma: divide os dados em intervalos (`num_bins`) e mostra quantos valores caem em cada um. Com 4 intervalos no exemplo (1 a 80), o primeiro intervalo tem 10 ocorrências e o terceiro tem 0.
- Pizza: `autopct` mostra o percentual, `explode` separa as fatias, `shadow` põe sombra e `startangle` gira o gráfico.
- Barras: duas pesquisas de datas diferentes para os mesmos candidatos, com o segundo grupo deslocado (`index + bar_width`) e `xticks` com os nomes. `barh` faz as barras na horizontal.

Código

###1
```python
import matplotlib.pyplot as plt
plt.plot((1,1,2,3,5,8))
plt.xlabel('Eixo X')
plt.ylabel('Eixo Y')
plt.show()
```

### valores de X e Y
```python
import matplotlib.pyplot as plt
plt.plot((1,2,3,4),(1,8,27,64))
plt.xlabel('Valor original')
plt.ylabel('Valor ao cubo')
plt.show()
```

### só pontos vermelhos
```python
import matplotlib.pyplot as plt
plt.plot((1,2,3,4),(1,8,27,64),'ro')
plt.xlabel('Valor original')
plt.ylabel('Valor ao cubo')
plt.show()
```

###outros estilos
```python
import matplotlib.pyplot as plt
plt.plot((1,2,3,4),(1,8,27,64),'gD')   # exemplo 4: losangos verdes
# plt.plot((1,2,3,4),(1,8,27,64),'m--')  # exemplo 5: linha tracejada magenta
plt.xlabel('Valor original')
plt.ylabel('Valor ao cubo')
plt.show()
```

###reta e pontos, título e limites dos eixos
```python
import matplotlib.pyplot as plt
eixox = (1,2,3,4)
eixoy = (1,8,27,64)
plt.plot(eixox,eixoy,'m--',eixox, eixoy, 'bo')
plt.title('Grafico contendo reta e pontos')
plt.xlabel('Valor original')
plt.ylabel('Valor ao cubo')
plt.xlim(0,5)      # exemplo 7
plt.ylim(0,100)    # exemplo 7
plt.show()
```

### histograma
```python
import matplotlib.pyplot as plt

x = [1,4,7,8,10,20,25,28,14,32,35,38,5,65,77,80,12,9]
num_bins = 4        # no exemplo 9 foi usado 8
plt.hist(x, num_bins, facecolor='green')
plt.show()
```

### pizza
```python
import matplotlib.pyplot as plt
labels = 'Pretos', 'Castanhos', 'Verdes', 'Azuis'
sizes = [70, 80, 20, 10]
plt.pie(sizes, labels=labels, autopct='%1.1f%%')
plt.axis('equal')
plt.show()
```

###pizza com formatação
```python
import matplotlib.pyplot as plt
labels = 'Pretos', 'Castanhos', 'Verdes', 'Azuis'
sizes = [70, 80, 20, 10]
explode = (0.03, 0.03, 0.03, 0.03)

plt.pie(sizes, explode=explode, labels=labels, autopct='%1.1f%%', shadow=True, startangle=90)
plt.axis('equal')
plt.show()
```

###barras (pesquisa eleitoral)
```python
import numpy as np
import matplotlib.pyplot as plt

grupos = 5
anterior = (30, 20, 18, 17, 15)
atual = (40, 20, 20, 10, 10)

index = np.arange(grupos)
bar_width = 0.3

barras1 = plt.bar(index, anterior, bar_width, color='r', label='10-10-2018')
barras2 = plt.bar(index + bar_width, atual, bar_width, color='b', label='17-10-2018')

plt.xlabel('Candidato')
plt.ylabel('Percentual')
plt.title('Pesquisa Eleitoral')
plt.xticks(index + bar_width, ('Leonardo', 'Maria', 'Ana', 'Outros', 'Indecisos'))
plt.legend()
plt.show()
```

### barras na horizontal
```python
import numpy as np
import matplotlib.pyplot as plt

grupos = 5
anterior = (30, 20, 18, 17, 15)
atual = (40, 20, 20, 10, 10)

index = np.arange(grupos)
bar_width = 0.3

barras1 = plt.barh(index, anterior, bar_width, color='r', label='10-10-2018')
barras2 = plt.barh(index + bar_width, atual, bar_width, color='b', label='17-10-2018')

plt.ylabel('Candidato')
plt.xlabel('Percentual')
plt.title('Pesquisa Eleitoral')
plt.yticks(index + bar_width, ('Leonardo', 'Maria', 'Ana', 'Outros', 'Indecisos'))
plt.legend()
plt.show()
```
