# Requisições Web

Com a biblioteca `requests` o Python acessa páginas e serviços da internet por HTTP e recebe a resposta para ser usada no programa.

## Conceitos
- Métodos HTTP mais comuns: GET (buscar dados) e POST (enviar dados)
- `status_code` indica o resultado (200 = sucesso)
- `resposta.text` traz o conteúdo da página (HTML) e `resposta.json()` converte respostas em JSON
- Combina bem com expressões regulares para extrair informações do HTML

## Exemplos e lugares aplicados
Coletar dados de sites, consumir APIs e extrair e-mails ou preços de páginas.

## Minhas anotações da aula
(Escreva aqui com suas palavras o que o professor explicou nesta aula.)

## Código

### Requisição da aula (página "Fale com o coordenador")
```python
import requests
requisicao = requests.post("https://www.uninove.br/graduacao/ciencia-da-computacao/fale-com-o-coordenador/")
print(requisicao.text)
```
O resultado é todo o HTML da página.

### Exemplo com GET
```python
import requests
resposta = requests.get("https://www.uninove.br")
print(resposta.status_code)   # 200 se deu certo
print(resposta.text[:200])    # primeiros 200 caracteres
```
