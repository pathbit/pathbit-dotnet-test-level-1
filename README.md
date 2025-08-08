# Recrutamento PATHBIT - Desafio de Desenvolvimento .NET Level 1

## Introdução

Este desafio propõe a construção de uma API REST em .NET, utilizando a linguagem C#, com enfoque em práticas de desenvolvimento, design de software e arquitetura de sistemas. O objetivo é desenvolver um sistema de gerenciamento de clientes e pedidos, aplicando conceitos modernos de programação e design arquitetônico.

## Importante

1. Você deve criar o CRUD para todas as entidades referenciadas neste projeto.
2. Você deve respeitar as regras obrigatórias, criar novas regras, endpoints e outros necessários paraa entrega do CRUD deste projeto.
3. Você pode e deve utilizar padrões de mercado e propor melhores soluções para resolver o problema apresentado, seja criativo.
4. Testes unitários são importantes e obrigatórios. Buscamos uma cobertura de testes mínima de 70% para este projeto.

## Tecnologias e Práticas Requeridas

- Utilização do .NET C# na versão 8 ou superior.
- Adoção de Orientação a Objetos, princípios SOLID e Clean Code.
- Implementação de testes unitários utilizando o framework xUnit.
- Uso de banco de dados PostgreSQL.
- Emprego do Entity Framework Core em sua última versão disponível.
- Proteção dos endpoints das APIs com autenticação Basic.
- Documentação da API com Swagger.
- Configuração de logs em arquivo texto (`./logs/application.log`), com os arquivos de log devidamente ignorados pelo sistema de controle de versão `.gitignore`.

## Estrutura do Projeto

A estrutura do projeto deve seguir o padrão Domain-Driven Design (DDD), organizada nas seguintes pastas:

- `./src`
  - `./Api`
  - `./Application`
  - `./Common`
  - `./Domain`
  - `./Infrastructure`
- `./tests/UnitTests`

## Desafio: Sistema de Gerenciamento de Clientes e Pedidos

### Entidades Principais:

- **User**: Detalhes do usuário incluindo ID (GUID), e-mail, nome de usuário, senha, e tipo do usuário (CLIENTE ou ADMINISTRADOR).
- **Customer**: Informações do cliente contendo ID (GUID), nome, e e-mail.
- **Product**: Dados do produto incluindo ID (GUID), nome, preço e quantidade disponível.
- **Order**: Detalhes do pedido com ID (GUID), data do pedido, status (ENVIADO), ID do cliente, ID do produto, quantidade, preço, CEP de entrega e endereço de entrega.
- _**OBSERVAÇÃO**: As entidades Order, Product e Customer devem estar interligadas por relações de chave estrangeira._

### Endpoints e Regras Obrigatórias:
> [1] Os IDs devem ser gerados automaticamente no formato `GUID`
> 
> [2] Você deve criar os demais endpoints e as demais regras que julgar necessárias
> 
> [3] AS REGRAS BAIXO SÃO OBRIGATÓRIAS E NÃO EXCLUEM REGRAS E ENDPOINTS QUE VOCÊ DEVE IMPLEMENTAR PARA UM PROJETO MAIS RESILIENTE E COMPLETO

- **POST /signup**: Cadastra clientes e usuários, armazenando a senha como hash SHA256.
  - Deve informar os dados que serão armazenados na tabela Customer e uma senha
  - O sistema deve armazenar os dados nas tabelas User (usuario=email, email e senha) e Customer (nome e email)
  - A senha deve ser armazenada como um hash usando SHA256
  - _**OBSERVAÇÃO**: Este endpoint não deve ser protegido pela autorização de JWT_

- **POST /login**: Autentica usuário e gera um Token JWT com duração de 01 HORA.
  - Deve informar o usuario e a senha
  - O sistema deve realizar o hash da senha e comparar os dados informados (usuario e senha) com os dados armazenados no banco de dados
  - O sistema deve gerar um Token JWT com validade de até 01 HORA para utilização nos demais endpoints com o seguintes dados (ID cliente, Nome e E-mail)
  - _**OBSERVAÇÃO**: Este endpoint não deve ser protegido pela autorização de JWT_

- **POST /products**: Restrito a usuários ADMINISTRADORES para cadastro de produtos.
  - Somente usuários do tipo ADMINSTRADOR podem cadastrar produtos
  - A quantidade do produto deve ser maior que zero e do tipo inteiro

- **POST /orders**: Exclusivo para CLIENTES, com regras específicas para validação de endereço, existência e quantidade de produto.
  - Somente usuários do tipo CLIENTE podem enviar ordens
  - No envio da ordem devemos buscar o endereço de entrega através do serviço viacep.com.br, se o endereço não existir o envio da ordem deve ser negado
  - No envio da ordem devemos usar a informação do ID do cliente que está no token
  - No envio da ordem deve ser validado se o produto informado existe
  - No envio da ordem deve ser validado se a quantidade disponível para o produto é maior que a quantidade da ordem
  - A quantidade disponível deve ser atualizada após a gravação de uma ordem no banco de dados, utilize transação para realizar esta regra com segurança

### Operações Específicas:

- Detalhamento de operações de gerenciamento de clientes, pedidos, e produtos.
- Validação e atualização segura de quantidades de produtos disponíveis.

### Critérios de Entrega:

- Código fonte hospedado no GitHub, com um `README.md` detalhando instruções de: execução do projeto local, execução do projeto no docker e avaliação da cobertura de testes.
- Documentação dos endpoints utilizando Swagger.
- Configuração para execução em Docker, incluindo `Dockerfile` e `docker-compose.yml`.
- Scripts de banco de dados localizados em `./scripts/db` para setup inicial.

### Avaliação:

O foco da avaliação será na estratégia adotada para o gerenciamento de pedidos, cobertura e qualidade dos testes unitários, qualidade do código, aderência aos princípios SOLID e Clean Code, modelagem e performance do banco de dados, uso correto dos verbos e status code HTTP, e tratamento de erros na API.

## Entrega
Ao concluir o desafio, disponibilize o código em um repositório Git publico pessoal em seu nome e envie o link para a equipe de recrutamento da PATHBIT. Documente os passos para execução do projeto e quaisquer outras informações que considere relevantes.

Boa sorte!
