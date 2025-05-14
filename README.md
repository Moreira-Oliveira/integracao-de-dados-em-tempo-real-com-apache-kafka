# Integracao-de-dados-em-tempo-real-com-Apache-Kafka

📚 Monitoramento de Criptomoedas em Tempo Real com Kafka, MongoDB e Streamlit

Neste   projeto   vou   mostrar   um   sistema   integrado   para   monitorar   o   mercado   de criptomoedas  em  tempo  real. Usaremos  o  Apache  Kafka  para  receber  dados  de  cotações  de criptomoedas através de API. De forma assíncrona vamos consumir os dados do Kafka, filtrar e armazenar no MongoDB, para então na sequência analisar e monitorar os dados em tempo real através de uma web app criada com Streamlit.

📚 Programas que irei utilizar

Coincap.io
![Image](https://github.com/user-attachments/assets/4f140a59-dcef-48b8-bc97-362c1bc012e5)

Apache Kafka
![Image](https://github.com/user-attachments/assets/aff7a80a-85b2-4a23-ab2f-b17f76364e55)

Mongodb
![Image](https://github.com/user-attachments/assets/8fab16b1-8df0-475f-bb48-502b5f369b23)

Docker Desktop
![Image](https://github.com/user-attachments/assets/31407703-1014-4478-ac95-f64456d8477d)

Streamlit
![Image](https://github.com/user-attachments/assets/cc675518-41eb-4616-bfab-d6e19bc16db2)

ZooKeeper
![Image](https://github.com/user-attachments/assets/a3e2b9fd-02f8-4758-8f3e-6e5c1b6a6d4e)




📚 Com tudo preparado vamos iniciar executando os arquivo em Python para da inicio ao projeto no Jupyter notebook (Todos os codigos vão esta disponiveis na pasta aqui no GitHub).

![Image](https://github.com/user-attachments/assets/b3a0166a-120e-486a-8c68-e0651f3b84bd)


Com isso vamos criar o tópico kaflka via código python, criar e executar o kaflka producer e criar a app de monitoramento com streaming.


📚 Projeto


1. Inicialização da Infraestrutura (Docker Compose)
O arquivo docker-compose.yml inicia três serviços essenciais:

Zookeeper (porta 2181):
Atua como coordenador do cluster Kafka, gerenciando configurações e sincronização entre nós. Usa a imagem Bitnami com autenticação anônima habilitada.

Kafka (porta 9092):

* Broker de mensagens configurado para:

Conectar ao Zookeeper em zookeeper:2181

Aceitar conexões não criptografadas (PLAINTEXT)

Expor o broker em localhost:9092 para aplicações externas

Problema atual: Falha na inicialização devido à configuração incompleta de listeners.

MongoDB (porta 27018 externa/27017 interna):
Banco de dados com:

Autenticação habilitada (usuário root, senha dsapassword)

Volume persistente em ./mongo-data

Problema observado: Reinicializações podem estar relacionadas a permissões no volume.

2. Configuração do Sistema

* O arquivo dsa_config.conf define:

Kafka: Endereço localhost:9092

API CoinCap: URL para obter cotações de criptomoedas

MongoDB: String de conexão com credenciais e porta mapeada

3. Fluxo de Processamento
Etapa 1: Criação do Tópico Kafka (Jupyter Notebook)
Objetivo: Criar o tópico dsa-p6-crypto-topic para armazenar mensagens.

Etapa 2: Producer Kafka (Jupyter Notebook)

* Funcionamento:

Coleta dados da API CoinCap (top 10 criptomoedas)

Adiciona timestamp

Envia para o tópico Kafka a cada 15 segundos

Etapa 3: Consumer Kafka (Jupyter Notebook)

* Funcionamento Ideal:

Consome mensagens do tópico

Remove o campo vwap24Hr (limpeza de dados)

Armazena no MongoDB na coleção dsa_p6_crypto_collection

Dependência:
Requer que o Producer esteja funcionando corretamente.

Etapa 4: Visualização com Streamlit
Processo:

Conecta ao MongoDB

Extrai dados históricos

* Gera visualizações com:

Gráfico de linhas interativo

Filtro por criptomoeda

Tabela com amostra dos dados

* Funcionalidades:

Exibe variação de preços ao longo do tempo

Atualizações em tempo real conforme novos dados chegam ao MongoDB. Tudo isso para implementar uma arquitetura completa de pipeline de dados em tempo real, desde a coleta até a visualização, sendo ideal para monitoramento financeiro de criptomoedas.





