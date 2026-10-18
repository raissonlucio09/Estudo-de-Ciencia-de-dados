# Estruturas de repetição

Estruturas de repetição (laços ou loops) executam um bloco de instruções várias vezes, enquanto uma condição for verdadeira ou para cada item de uma sequência.

 Conceitos
- `while`: repete enquanto a condição for verdadeira
- `for`: repete para cada elemento de uma sequência (lista, texto, `range()`)
- `range(inicio, fim, passo)`: gera números e o valor `fim` não entra
- `break` interrompe o laço e `continue` pula para a próxima repetição
- Cuidado com laço infinito: a condição do `while` precisa mudar dentro do bloco

 Exemplos e lugares aplicados
Somar valores, percorrer listas, repetir a leitura de dados até o usuário digitar algo válido, gerar tabelas.



## Código

### for com range
```python
for i in range(1, 6):
    print(i)
```
Saída: `1 2 3 4 5`, um por linha.

### while
```python
contador = 1
while contador <= 5:
    print(contador)
    contador = contador + 1
```

### Soma de 1 a 10 com break e continue
```python
soma = 0
for n in range(1, 11):
    if n == 3:
        continue   # pula o 3
    if n == 9:
        break      # para no 9
    soma = soma + n
print(soma)
```
Saída: `33` (1+2+4+5+6+7+8)
