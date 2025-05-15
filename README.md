# Integracao-de-dados-em-tempo-real-com-Apache-Kafka

📚 Monitoramento de Criptomoedas em Tempo Real com Kafka, MongoDB e Streamlit

Neste projeto, vou mostrar um sistema integrado para monitorar o mercado de criptomoedas em tempo real. Usaremos o Apache Kafka para receber dados de cotações de criptomoedas através de uma API. De forma assíncrona, vamos consumir os dados do Kafka, filtrar e armazenar no MongoDB, para então, na sequência, analisar e monitorar os dados em tempo real através de um aplicativo web criado com Streamlit

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




📚 Com tudo preparado, iniciamos executando os arquivos Python no Jupyter Notebook para dar início ao projeto. Todos os códigos estão disponíveis na pasta correspondente aqui no GitHub.

![Image](https://github.com/user-attachments/assets/ed0573ff-ab8d-4096-aac0-643d7fc2c662)


Neste processo, criamos o tópico Kafka via código Python, implementamos e executamos o Kafka Producer e desenvolvemos a aplicação de monitoramento com Streamlit.


📚 Estrutura do Projeto


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

Exibe variação de preços ao longo do tempo.

Atualizações em tempo real conforme novos dados chegam ao MongoDB. Tudo isso para implementar uma arquitetura completa de pipeline de dados em tempo real, desde a coleta até a visualização, sendo ideal para monitoramento financeiro de criptomoedas.


📚 Execução Final


Ao executar todos os scripts, iniciamos o projeto6-app. O código cria um aplicativo interativo que permite aos usuários monitorarem os preços das criptomoedas em tempo real. Ele se conecta ao MongoDB para buscar dados históricos, aplica filtros com base na criptomoeda selecionada pelo usuário e apresenta essas informações em gráficos e tabelas. Dessa forma, proporciona uma experiência visual clara e prática para acompanhar as flutuações de preços ao longo do tempo.

![Image](https://github.com/user-attachments/assets/66c64019-8c7f-41dd-a73f-fb5554b9796d)


📚 Conclusão

Este projeto demonstrou como integrar diversas tecnologias — Kafka, MongoDB, Docker e Streamlit — para construir uma solução robusta de monitoramento em tempo real de criptomoedas. A arquitetura criada permite desde a coleta contínua de dados por API, processamento e armazenamento eficiente, até a visualização dinâmica e interativa dos dados. Essa abordagem pode ser facilmente adaptada para outros contextos que exijam análise de dados em tempo real, reforçando o poder das ferramentas open source na criação de pipelines modernos e escaláveis.

