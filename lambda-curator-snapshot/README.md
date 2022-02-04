# lambda-curator - Inicializador do Elasticsearch Curator para o AWS Lambda..

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
- __AWS_ACCESS_KEY_ID__: o ID da chave de acesso do aws.
- __AWS_SECRET_ACCESS_KEY__: a chave de acesso secreta do aws.
- __AWS_REGION__: a região aws.


## Package function
```
make package
```
This will create a _FUNCTION_NAME.zip_ including the bootstrap.py (and all Curator dependencies) and actions.yml.

## Push package to function
```
make awspush
```
Isso criará um _FUNCTION_NAME.zip_, incluindo o bootstrap.py (e todas as dependências do Curator) e actions.yml.

## Update package function
```
make awsupdate
```
Isso criará e publicará a função lambda-curator.

## Connecting to an AWS Elasticsearch cluster
A função lambda-curator assinará todas as solicitações com as credenciais da AWS da função de execução (IAM_ROLE). Conceder a essa função acesso ao cluster do AWS Elasticsearch usando o IAM autenticará todas as ações do curador lambda _automagicamente_.