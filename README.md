# Recuperação da Informação: Amazon Fine Food Reviews

## Sobre o Projeto
Ter que ler mais de meio milhão de avaliações de comida para descobrir quais produtos causaram algum tipo de problema de saúde nos clientes seria humanamente impossível, certo?

Este projeto resolve exatamente esse problema. Construí um pipeline de **Recuperação da Informação (RI)** para varrer um dataset gigante da Amazon (+568 mil reviews) e identificar automaticamente relatos críticos de segurança alimentar. 

Em vez de usar uma simples busca por palavras-chave, que traz muito "ruído" e resultados irrelevantes, implementei algoritmos probabilísticos clássicos. O objetivo foi testar se modelos matemáticos conseguem entender o peso correto das palavras e ranquear as reclamações mais perigosas no topo da busca.

## Como funciona por baixo dos panos?
Para fugir do viés das palavras mais frequentes, a análise foi construída em cima de dois modelos:
* **TF-IDF:** Para entender a raridade e a importância de termos específicos como "intoxicação", "hospital", "estragado", dentro de todo o universo de avaliações.
* **BM25:** Uma evolução do TF-IDF que lida muito melhor com o tamanho dos textos, evitando que reviews gigantescas tenham vantagem injusta sobre reclamações curtas e diretas.

## Tecnologias e Ferramentas
Todo o desenvolvimento foi feito em **R**, com foco em processamento eficiente:
* `data.table`: Leitura e manipulação vetorizada super rápida do CSV pesado.
* `dplyr` e `tidytext`: Limpeza e tokenização dos textos.
* `SnowballC`: Aplicação de *stemming* (redução das palavras ao seu radical).
* `ggplot2`: Visualização de dados da análise exploratória.

## Automação da Base de Dados
Como o dataset original tem quase 300MB, seria uma péssima prática subi-lo para o GitHub. Para resolver isso e garantir a reprodutibilidade, o notebook possui um script inicial que consome a **API do Kaggle** e faz o download, extração e carregamento dos dados de forma 100% automatizada.

### Como rodar você mesmo:
Se quiser executar o notebook localmente ou no seu Google Colab, você só precisa das suas credenciais do Kaggle:
1. Crie ou acesse sua conta no [Kaggle](https://www.kaggle.com/).
2. Vá nas configurações do perfil e clique em **Create New Token** para baixar o arquivo `kaggle.json`.
3. Faça o upload desse arquivo para o seu ambiente de execução. O script da Seção 1 do notebook vai cuidar do resto (configuração de pastas, permissões e download do `.zip`).
