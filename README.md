# Inicializador do Elasticsearch Curator para o AWS Lambda

Este é um bootstrapper simples para executar o [Elasticsearch Curator] (https://github.com/elastic/curator) como uma função _AWS Lambda_. As funções do Lambda podem ser acionadas usando _CloudWatch Events_, tornando-o um ambiente adequado para a execução de tarefas do Curator.

## Configuração
### Variáveis ​​ambientais
- __ES_HOST__: o URL base do cluster Elasticsearh.
- __ES_PORT__: a porta do cluster Elasticseach (padrão: 443).
- __DRY_RUN__: define o sinalizador Curator _-- dry-run_ (padrão: True)
- __FUNCTION_NAME__: o nome da função lambda.
- __IAM_ROLE__: a função de execução da função lambda.

### AWS CLI
O [AWS CLI] (https://aws.amazon.com/cli/) precisa ser instalado para enviar / atualizar a função _lambda-curator_. No mínimo, as seguintes variáveis ​​precisam ser definidas:
- __AWS_ACCESS_KEY_ID__: ID da chave de acesso do aws.
- __AWS_SECRET_ACCESS_KEY__: chave de acesso secreta do aws.
- __AWS_REGION__: região da aws.


## Package function
```
make package
```
Isto criará um _FUNCTION_NAME.zip_ incluindo o actions.yml e o bootstrap.py, assim como todas as dependencias do Curator.

## Push package to function
```
make awspush
```
Isso cria/altera o código da função Lambda na AWS.

## Update package function
```
make awsupdate
```
Isso criará e publicará a função lambda-curator.

## Connecting to an AWS Elasticsearch cluster
A função lambda-curator assinará todas as solicitações com as credenciais da AWS da função de execução (IAM_ROLE). Conceder a essa função acesso ao cluster do AWS Elasticsearch usando o IAM autenticará todas as ações do curador lambda _automagicamente_.
