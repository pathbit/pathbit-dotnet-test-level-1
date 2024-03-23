# Recrutamento PATHBIT - Desafio de Desenvolvimento .NET Level 1 (Versão 1.0)

## Introdução

Desenvolva uma solução em C# .NET 6 (ou superior) composta por uma WebAPI, uma WebApplication e um Serviço para disparo de emails.

## Especificação

### Projetos

1. **WebAPI**: Integração da aplicação, oferecendo o serviço de cadastro.
2. **WebApplication**: Interface web para realização do cadastro do cliente.
3. **Serviço de Disparo de Email**: Envia email de notificação após conclusão do cadastro.

### Cadastro

O cadastro do cliente será dividido em 4 partes:

1. **Dados básicos**
    - Nome
    - Data de nascimento
    - CPF
    - Email
    - Telefone
2. **Dados financeiros**
    - Renda
    - Patrimônio
3. **Dados de endereço**
    - Rua
    - Número
    - Bairro
    - Cidade
    - Estado
    - CEP
4. **Dados de segurança**
    - Senha
    - Confirmação de senha

#### Requisitos da API

- Armazene os dados cadastrais em um banco de dados MongoDB. Use [MongoDB Atlas](https://www.mongodb.com/free-cloud-database) gratuito ou Docker local.
- Consulte o CEP no serviço [CepRapido.com](https://ceprapido.com/api/docs).
- Valide:
    - CPF
    - Se o cliente é maior de idade conforme regras brasileiras
    - Formato de email e telefone
    - Renda + Patrimônio > 1000,00
- Armazene apenas o HASH da senha no banco de dados.
- Após conclusão do cadastro, envie uma mensagem para a fila `cadastro.em.analise.email` do RabbitMQ. Use [CloudAMQP](https://www.cloudamqp.com/) gratuito ou Docker local.

#### Requisitos da WebApplication

- Use qualquer framework web (ASP.NET Razor Pages, WebForms, Pure HTML5, React, Angular, etc.).
- Divida o cadastro conforme os 4 passos informados.
- Após a última etapa, direcione o usuário para uma página informando que o cadastro está em análise.

#### Requisitos do Serviço de Disparo de Email

- Conecte-se à fila `cadastro.em.analise.email` do RabbitMQ.
- Ao receber uma mensagem, envie um email para o cliente:

    ```
    Olá {{nome}},

    O seu cadastro está em análise e em breve você receberá um e-mail com novas atualizações sobre seu cadastro.

    Atenciosamente,

    Equipe PATHBIT
    ```

- Use [SendGrid](https://sendgrid.com/free/) ou [Mailgun](https://signup.mailgun.com/new/signup) para envio dos emails.

## Entrega

Ao concluir o desafio, organize o código em um repositório Git e envie o link para a equipe de recrutamento. Documente os passos para execução do projeto e quaisquer outras informações que considere relevantes.

Boa sorte!
