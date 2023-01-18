# Verificações SEO
Algumas verificações úteis para otimizações em SEO, arquivo no colab: https://colab.research.google.com/drive/1e5GmHsksIVtq-kjqMbLxLlUcwq2EAZ0f

## **Contagem de Palavras**
Aqui selecionamos o elemento **article**, e pegamos o texto dentro desse elemento. Em seguida, dividimos o texto em uma lista de palavras usando o método `split()` e contamos o número de palavras usando a função `len()`. Por fim, imprimimos a contagem de palavras na tela.

```
from bs4 import BeautifulSoup
import requests

url = input("Digite a URL e aperte ENTER: ")
response = requests.get(url)
soup = BeautifulSoup(response.text, 'html.parser')

# Encontra o elemento <article>
article = soup.find('article')

# Verifica se o elemento foi encontrado
if article:
  text = article.get_text() # Pega o texto dentro do elemento "article"
  word_count = len(text.split())
  print("A URL possui", word_count, "palavras.")
else:
    print("Não foi possível encontrar o elemento <article> na página, altere para body ou algum elemento apropriado para a estrutura do seu site.")
```


## **Densidade de Palavra-Chave**
Aqui selecionamos o elemento **article**, pegamos o texto dentro desse elemento e contamos a quantidade de palavras e a quantidade de vezes que a palavra-chave possue na página. Então calculamos a densidade da palavra-chave com base no total de palavras dentro do elemento e imprime a densidade na tela.

```
from bs4 import BeautifulSoup
import requests

url = input("Digite a URL e aperte ENTER: ")
keyword = input("Digite a palavra-chave: ")
response = requests.get(url)
soup = BeautifulSoup(response.text, 'html.parser')

# Encontra o elemento <article>
article = soup.find('article')

# Verifica se o elemento foi encontrado
if article:
    # Obtém o texto dentro do elemento <article>
    text = article.text
    word_count = len(text.split())
    keyword_count = text.count(keyword)
    density = (keyword_count / word_count) * 100
    print("A densidade da palavra-chave '" + keyword + "' é de " + str(density) + "%")
else:
    print("Não foi possível encontrar o elemento <article> na página, altere para body ou algum elemento apropriado para a estrutura do seu site.")
```

## **Links nofollow** 
Aqui verificamos a quantidade de URLs que possui a página e listamos os links que possuem o atributo `rel="nofollow"`

```
from bs4 import BeautifulSoup
import pandas as pd
import requests

url = input("Digite a URL e aperte ENTER: ")
response = requests.get(url)
soup = BeautifulSoup(response.text, 'html.parser')

# Utiliza o método find_all() do BeautifulSoup para encontrar todos os links 'a'
links = soup.find_all('a')

# Armazena o total de links encontrados
total_links = len(links)

# Cria um contador para armazenar o número de links com o atributo rel='nofollow'
nofollow_links = 0

# Cria uma lista para armazenar os links com o atributo rel='nofollow'
nofollow_links_list = []
for link in links:
    if 'rel' in link.attrs and link['rel'] == ['nofollow']:
        nofollow_links += 1
        nofollow_links_list.append(link.get("href"))

print("A URL possui um total de", total_links, "links. E possui", nofollow_links, "links com o atributo rel='nofollow'.")
print("Lista de links rel='nofollow':",nofollow_links_list)
```
