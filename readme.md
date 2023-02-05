# Pré-requisitos

Implante um Ubuntu 20.04 Server totalmente atualizado com pelo menos 4 GB de RAM .      
Crie um usuário não raiz com acesso sudo.


#### 1. Instale o OpenJDK

Instale o OpenJDK exigido pelo Elasticsearch e outras dependências.     
```
sudo apt -y install bash-completion apt-transport-https uuid-runtime pwgen openjdk-17-jre-headless
```
#### 2. Instale o Elasticsearch

Importe a chave de assinatura Elasticsearch PGP.
```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add -
```
Adicione o repositório Elasticsearch.
```
echo "deb https://artifacts.elastic.co/packages/oss-6.x/apt stable main" | sudo tee -a /etc/apt/sources.list.d/elastic-6.x.list
```
Atualize o sistema.
```
sudo apt update
```
Instale o Elasticsearch.
```
sudo apt -y install elasticsearch-oss
```
Edite o arquivo de configuração do Elasticsearch.
```
sudo vim /etc/elasticsearch/elasticsearch.yml
```
Adicione essas duas linhas ao final do arquivo.
```
cluster.name: graylog     
action.auto_create_index: false
```
Salve e saia do arquivo.
Recarregue o daemon do sistema.
```
sudo systemctl daemon-reload
```
Reinicie o serviço Elasticsearch.
```
sudo systemctl restart elasticsearch
```
Habilite o Elasticsearch para ser executado na inicialização do sistema.
```
sudo systemctl enable elasticsearch
```

#### 3. Instale o MongoDB
