# Estatística: Análise Exploratória dos dados e Regressão

A análise exploratória de dados (AED ou EDA) é a fase de observar os dados, sem uma hipótese definida, para encontrar padrões, relações e anomalias. A regressão descreve por um modelo matemático a relação entre variáveis e permite fazer previsões.

Conceitos
- AED foi promovida por John Tukey: a hipótese é o ponto de chegada da análise, e não o ponto de partida
- Ferramentas: histograma, diagrama de caixa, diagrama de Pareto (80/20), gráfico de dispersão, diagrama de ramos e folhas, entre outras
- Ciência de dados: converter dados brutos em informação para decisões baseadas em fatos
- Regressão: variável dependente (Y, a que se quer estimar) e variáveis independentes (X)
- Simples (1 variável independente) ou múltipla (mais de uma); linear ou não linear
- Funções comuns: reta `Y = aX + b`, parábola `Y = aX² + bX + c` e logarítmica `Y = a·log(X) + b`
- Modelos preditivos usam dados históricos e funções de regressão para prever o futuro

Exemplos e lugares aplicados
Previsão de evasão de alunos, de lotação de transporte e de falha de equipamentos; análise de vendas (caso muito citado de fraldas e cerveja em uma rede de varejo).

Minhas anotações da aula
- Na estatística tradicional: cria-se a hipótese, coletam-se os dados e valida-se a hipótese. Na AED: analisam-se os dados, encontram-se padrões e só depois formulam-se hipóteses para testar.
- Caso do varejo (fraldas e cerveja): é uma história muito contada, mas não há consenso sobre ter acontecido exatamente assim.
- Regressão linear é "linear" nos parâmetros: `Y = aX + bX² + c` é linear em a, b e c, mesmo sendo uma parábola no gráfico. `Y = a·e^(bX)` não é linear nos parâmetros.
- Cuidado com extrapolar: assumir sempre uma reta pode levar a conclusões absurdas (exemplos da aula: população carcerária dobrando a cada 8 anos e 100% dos americanos acima do peso em 2048). É preciso escolher a função adequada ao fenômeno.


