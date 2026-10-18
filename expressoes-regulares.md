# Expressões Regulares

Uma expressão regular (regex) é uma forma flexível e concisa de localizar cadeias de caracteres que seguem um padrão, como e-mails, telefones e endereços IP. Em Python usa-se o módulo `re`.

## Conceitos
- `re.match()` procura o padrão só no início da string; `re.search()` procura em toda a string; `re.findall()` devolve todas as ocorrências em uma lista
- Quando não encontra, `match` e `search` retornam `None`
- RAW string (`r"..."`): a barra invertida é tratada como texto puro, sem caracteres especiais como `\n`
- `\w` = qualquer letra ou número, `\d` = qualquer dígito
- Quantificadores: `+` (1 ou mais), `*` (0 ou mais), `{n}` (exatamente n), `{n,m}` (de n a m)
- `[ ]` indica um conjunto de opções, como `[\w\.-]`
- `.group()` mostra o trecho encontrado

## Exemplos e lugares aplicados
Extrair e-mails de páginas HTML, validar telefones e CPFs, localizar padrões em textos grandes.

## Minhas anotações da aula
- `match` só acha o texto no começo da string; `search` acha em qualquer lugar. Se não achar, ambos retornam `None`.
- Em RAW string o `\n` aparece como texto e não pula linha.
- `\w\w\w\w\w\w` acha 6 caracteres seguidos; `\w+` pega a palavra inteira; `\w{6,8}` limita de 6 a 8 caracteres; `\d+` pega o número inteiro.
- Para números com ponto, usar `\d+\.\d+` e, se não achar, `\d+`.
- `search` para na primeira ocorrência; para todas, usar `findall`.
- Padrão de e-mail da aula: começa com `mailto:` (para ignorar a segunda ocorrência do e-mail na página), depois letras, números, pontos ou traços, o `@`, o domínio, um ponto e uma terminação de 2 a 3 caracteres. `x[7:]` remove o `mailto:`.

## Código

### Exemplo 1: match e search
```python
import re

string = "O aluno José foi reprovado. A aluna Ana foi aprovada e os alunos Thiago e Andre ficaram em dependência"

procurar = re.match("O aluno",string)
print(procurar)
procurar = re.match("Ana",string)
print(procurar)
procurar = re.search("O aluno",string)
print(procurar)
procurar = re.search("Ana",string)
print(procurar)
procurar = re.search("Monica",string)
print(procurar)
```
Saída:
```
<re.Match object; span=(0, 7), match='O aluno'>
None
<re.Match object; span=(0, 7), match='O aluno'>
<re.Match object; span=(36, 39), match='Ana'>
None
```

### Exemplo 2: RAW string
```python
print("Leonardo\nFernanda")
print(r"Leonardo\nFernanda")
```
Saída:
```
Leonardo
Fernanda
Leonardo\nFernanda
```

### Exemplo 3: \w, \d, + e {}
Na aula cada busca repetia um bloco `if/else`; aqui está a mesma ideia com um laço.
```python
import re

string = "O aluno José foi reprovado. Ele tirou 10 na segunda nota"

padroes = [r"\w\w\w\w\w\w", r"\d", r"\w\w\w\w\w\w+", r"\w{6,8}", r"\w{5}\w+", r"\d+"]
for padrao in padroes:
    procurar = re.search(padrao, string)
    if (procurar):
        print(procurar.group())
    else:
        print("Nao encontrado")
```
Saída:
```
reprov
1
reprovado
reprovad
reprovado
10
```

Para notas com ponto decimal:
```python
procurar = re.search(r"\d+\.\d+",string)
if (procurar):
    print(procurar.group())
else:
    procurar = re.search(r"\d+", string)
    if (procurar):
        print(procurar.group())
    else:
        print("Nao encontrado")
```

### Exemplo 4: findall
```python
import re

string = "O aluno José foi reprovado. Ele tirou 7.7 na segunda nota"

procurar = re.findall(r"\w\w\w\w+",string)
if (procurar):
    for x in procurar:
        print(x)
else:
    print("Nao encontrado")
```
Saída: `aluno`, `José`, `reprovado`, `tirou`, `segunda`, `nota` (uma por linha).

### Exemplos 5 e 6: e-mails de uma página
```python
import re
import requests

requisicao = requests.post("https://www.uninove.br/graduacao/ciencia-da-computacao/fale-com-o-coordenador/")
string_de_retorno = requisicao.text

padrao = re.findall(r'mailto:\w[\w\.-]+@[\w-]+\.[\w\.-]*\w{2,3}',string_de_retorno)
for x in padrao:
    print(x)
    comprimento = len(x)
    print (x[7:comprimento])
```
Saída na época da aula (depende do conteúdo atual da página):
```
mailto:cleber.vf@uninove.br
cleber.vf@uninove.br
mailto:ovidio@uninove.br
ovidio@uninove.br
```
