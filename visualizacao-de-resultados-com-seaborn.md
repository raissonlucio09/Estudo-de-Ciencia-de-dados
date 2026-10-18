# Visualização de resultados com Seaborn

O Seaborn é uma biblioteca de visualização de dados baseada no Matplotlib, com uma interface de alto nível para gráficos mais atraentes e informativos. Nesta aula também foram vistos gráficos 3D com o `mpl_toolkits.mplot3d`.

Conceitos
- `sns.load_dataset("iris")` carrega um conjunto de dados de exemplo (flores iris, com 3 espécies)
- `sns.swarmplot()` mostra os pontos de cada categoria sem sobreposição
- `sns.set()` aplica o estilo do Seaborn aos gráficos do Matplotlib; `plt.style.use('classic')` volta ao estilo padrão do Matplotlib
- Gráficos 3D: `projection='3d'`, `ax.scatter()` (pontos) e `ax.plot_trisurf()` (superfície)
- `np.cumsum()` soma acumulada, `np.linspace()` valores igualmente espaçados

Exemplos e lugares aplicados
Relatórios de análise de dados com visual mais agradável, comparação de categorias e visualização de dados em três dimensões.

Minhas anotações da aula
- Exemplo 1: no gráfico das iris, a espécie setosa tem as menores pétalas e a virginica as maiores.
- Exemplos 2 e 3 geram o mesmo gráfico; a diferença é só ligar o estilo do Seaborn (`sns.set()`), e a diferença visual é grande.
- Os exemplos 4 e 5 (histograma e barras) são os mesmos do Matplotlib, agora com o estilo do Seaborn.
- Exemplo 6: gráfico 3D de pontos com X de 0 a 10 e Y e Z aleatórios. Exemplo 7: superfície 3D de um conjunto de dados lido por URL com o Pandas.

## Código

### swarmplot
```python
import seaborn as sns
import matplotlib.pyplot as plt

iris = sns.load_dataset("iris")
sns.swarmplot(x="species", y="petal_length", data=iris)
plt.show()
```
Observação: o `load_dataset` baixa o conjunto de dados da internet na primeira vez. Em versões novas do Seaborn pode ser preciso usar `hue="species"` junto para evitar avisos.

### Matplotlib puro
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd

plt.style.use('classic')
rng = np.random.RandomState(0)
x = np.linspace(0, 10, 100)
y = np.cumsum(rng.randn(100, 5), 0)
plt.plot(x, y)
plt.legend('ABCDE', ncol=2, loc='upper left')
plt.show()
```

### com o estilo do Seaborn
```python
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import seaborn as sns

sns.set()
rng = np.random.RandomState(0)
x = np.linspace(0, 10, 100)
y = np.cumsum(rng.randn(100, 5), 0)
plt.plot(x, y)
plt.legend('ABCDE', ncol=2, loc='upper left')
plt.show()
```

### histograma com Seaborn
```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.set()
x = [1,4,7,8,10,20,25,28,14,32,35,38,5,65,77,80,12,9]
num_bins = 8
plt.hist(x, num_bins, facecolor='green')
plt.show()
```

### barras com Seaborn
```python
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns

sns.set()
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

### gráfico 3D de pontos
```python
import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

plt.style.use('classic')
rng = np.random.RandomState(5)
X = np.linspace(0, 10, 300)
Y = rng.rand(300, 1)
Z = rng.rand(300, 1)
ax = plt.figure().add_subplot(111, projection='3d')

ax.scatter(X, Y, Z, color='r')
ax.set_xlabel('Eixo X')
ax.set_ylabel('Eixo Y')
ax.set_zlabel('Eixo Z')

plt.show()
```

### superfície 3D (exemplo do Python Graph Gallery)
```python
from mpl_toolkits.mplot3d import Axes3D
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns

# dados (arquivo csv hospedado na web)
url = 'https://python-graph-gallery.com/wp-content/uploads/volcano.csv'
data = pd.read_csv(url)

# transformar para formato longo
df = data.unstack().reset_index()
df.columns = ["X","Y","Z"]

# transformar o nome antigo da coluna em algo numérico
df['X'] = pd.Categorical(df['X'])
df['X'] = df['X'].cat.codes

# gráfico
fig = plt.figure()
ax = fig.add_subplot(projection='3d')   # na aula: fig.gca(projection='3d') (removido nas versões novas)
ax.plot_trisurf(df['Y'], df['X'], df['Z'], cmap=plt.cm.viridis, linewidth=0.2)
plt.show()

# com barra de cores
surf = ax.plot_trisurf(df['Y'], df['X'], df['Z'], cmap=plt.cm.viridis, linewidth=0.2)
fig.colorbar(surf, shrink=0.5, aspect=5)
plt.show()

# girar
ax.view_init(30, 45)
plt.show()

# outra paleta
ax.plot_trisurf(df['Y'], df['X'], df['Z'], cmap=plt.cm.jet, linewidth=0.01)
plt.show()
```

