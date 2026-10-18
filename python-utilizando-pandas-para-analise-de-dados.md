# Python: Utilizando Pandas para análise de dados

Este tópico trabalha séries temporais em Python com a biblioteca Pandas (leitura dos dados) e o pacote Statsmodels (análise e previsão). Séries temporais têm sazonalidade, característica que a regressão comum não trata.

Conceitos
- `read_csv` do Pandas lê o arquivo e trata as datas (essenciais em séries temporais)
- `matplotlib` desenha o gráfico da série; `truncate()` mostra só um período
- `SARIMAX` (statsmodels): modelo ARIMA com sazonalidade; `order=(p,d,q)` e `seasonal_order=(P,D,Q,s)`, onde `s` é a sazonalidade (12 para dados mensais)
- `fit()` ajusta o modelo e `predict(start, end)` faz a previsão
- AIC: quanto menor, mais preciso o modelo; é usado para escolher os melhores parâmetros

 Exemplos e lugares aplicados
Previsão de vendas com sazonalidade (como flores no Dia das Mães), demanda, consumo e estoque.

Minhas anotações da aula
- Os dados do exemplo são vendas mensais de flores de 2001 a 2018, em arquivo `serietemporal.csv` (datas no formato AA-MM), com maio muito acima dos outros meses e crescimento de cerca de 10% ao ano. O arquivo é material complementar da aula.
- O gráfico mostra a sazonalidade (o padrão se repete todo ano) e uma tendência de crescimento.
- No exemplo 3, o modelo foi comparado com valores conhecidos (2011 a 2018) e depois previu 2019, com diferença menor que 0,2% em relação à planilha. Os dados foram criados com regras fixas; no mundo real o erro tende a ser maior.
- No exemplo 4 foram testadas todas as combinações de 0 e 1 para `order` e `seasonal_order`: o menor AIC foi cerca de 117, com `order=(1,0,0)` e `seasonal_order=(1,0,1,12)`, melhor que o AIC de cerca de 244 do exemplo 3.

## Código

### Dados iniciais (primeiro ano)
```
Ano-mês   Valor
01-01     100
01-02     115
01-03     170
01-04     160
01-05     300
01-06     155
01-07     150
01-08     167
01-09     157
01-10     170
01-11     179
01-12     250
```

### leitura e gráfico
```python
from pandas import read_csv
from pandas import datetime
from matplotlib import pyplot

def parser(x):
    return datetime.strptime('20'+x, '%Y-%m')

serie = read_csv('c:\\teste\\serietemporal.csv', header=0, parse_dates=[0], index_col=0, squeeze=True, date_parser=parser)
serie.plot()                                            # exemplo 1: todos os anos
# serie.truncate(before="2001-01", after="2002-12").plot()   # exemplo 2: só 2001 e 2002
pyplot.show()
```

Observação de compatibilidade: em versões novas do Pandas (2.x) `from pandas import datetime`, `squeeze=True` e `date_parser` não funcionam mais. A leitura equivalente é:
```python
from pandas import read_csv
from matplotlib import pyplot

serie = read_csv('serietemporal.csv', header=0, index_col=0, parse_dates=[0], date_format='%y-%m').squeeze("columns")
serie.plot()
pyplot.show()
```

### SARIMAX e previsão
```python
from pandas import read_csv
from pandas import datetime
import statsmodels.api as sm

def parser(x):
    return datetime.strptime('20'+x, '%Y-%m')

serie = read_csv('c:\\teste\\serietemporal.csv', header=0, parse_dates=[0], index_col=0, squeeze=True, date_parser=parser)
treino = serie.values
comparacao = treino[120:len(treino)]
modelo = sm.tsa.statespace.SARIMAX(treino, order=(2,1,1), seasonal_order=(1,1,1,12),
                                   enforce_stationarity=False, enforce_invertibility=False)
modelo_fit = modelo.fit()
print(modelo_fit.aic)

# comparar previsto x esperado de jan/2011 a dez/2018
indice_inicial = 12*10
indice_final = 12*18
i = 0
forecast = modelo_fit.predict(start=indice_inicial, end=indice_final)
for t in range(len(comparacao)):
    predito = forecast[i]
    esperado = comparacao[t]
    print('predito=%f, esperado=%f' % (predito, esperado))
    i = i + 1

# prever 2019
indice_inicial = 12*18
indice_final = 12*19
forecast = modelo_fit.predict(start=indice_inicial, end=indice_final)
for i in range(12):
    valorpredito = forecast[i]
    print('Valor Predito=%f' % (valorpredito))
```
Saída (trecho):
```
244.3846122754614
predito=259.473536, esperado=259.000000
predito=297.882908, esperado=298.000000
predito=440.987451, esperado=441.000000
...
Valor Predito=555.419260
Valor Predito=639.072398
Valor Predito=944.889367
...
Valor Predito=1390.480965
```

Previsto x planilha para 2019:

| Predito | Planilha |
|---|---|
| 555.42 | 556 |
| 639.07 | 639 |
| 944.89 | 945 |
| 889.93 | 890 |
| 1667.67 | 1668 |
| 861.28 | 862 |
| 833.77 | 834 |
| 928.40 | 929 |
| 873.43 | 873 |
| 944.89 | 945 |
| 995.52 | 995 |
| 1390.48 | 1390 |

### escolher os melhores parâmetros pelo AIC
```python
from pandas import read_csv
from pandas import datetime
import statsmodels.api as sm

def parser(x):
    return datetime.strptime('20'+x, '%Y-%m')

serie = read_csv('c:\\teste\\serietemporal.csv', header=0, parse_dates=[0], index_col=0, squeeze=True, date_parser=parser)
X = serie.values
tamanhototal = int(len(X) * 1)
treino = X[0:tamanhototal]
menorvalor = 999999999

for p1 in range(0,2):
 for d1 in range(0,2):
  for q1 in range(0,2):
   for p2 in range(0,2):
    for d2 in range(0,2):
     for q2 in range(0,2):
      param = (p1,d1,q1)
      param_seasonal = (p2,d2,q2,12)
      mod = sm.tsa.statespace.SARIMAX(treino,order=param,seasonal_order=param_seasonal,
                                      enforce_stationarity=False,enforce_invertibility=False)
      results = mod.fit()
      print("Order:",param,"Seasonal Order:", param_seasonal,"AIC:", results.aic)
      if (results.aic<menorvalor):
         menorvalor = results.aic
         melhorordem = param
         melhorordemsazonal = param_seasonal

print(menorvalor)
print(melhorordem)
print(melhorordemsazonal)
```
Saída final:
```
117.05702074130974
(1, 0, 0)
(1, 0, 1, 12)
```
