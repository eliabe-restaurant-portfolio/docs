# 🏗️ Arquitetura

Este projeto segue uma arquitetura **modular** e **orientada a domínio**.

## 🧱 Separação de Camadas e Responsabilidades

* `cmd/`: Pontos de entrada da aplicação (ex: `main.go` para **HTTP** e **migrações**).
* `internal/`: Código de **domínio** e **infraestrutura**, dividido em submódulos:
    * `adapters/`: Composição de dependências (**injeção de repositórios**, **middlewares**, etc).
    * `aggregates/`: **Agregados do domínio**, encapsulando **regras de negócio**.
    * `app/`: Inicialização da aplicação.
    * `connections/`: Gerenciamento de conexões externas (**Postgres**, **RabbitMQ**).
    * `entities/`: **Entidades** persistidas no banco de dados.
    * `envs/`: Gerenciamento de **variáveis de ambiente**.
    * `handlers/`: **Controladores HTTP** (camada de **apresentação**).
    * `middlewares/`: **Middlewares** do Gin (ex: autenticação **JWT**).
    * `queues/`: Integração com **filas** (**RabbitMQ**), incluindo **producers** e **consumers**.
    * `repositories/`: Implementação dos **repositórios** (acesso a dados).
    * `unit-of-work/`: Gerenciamento de **transações**.
    * `use-cases/`: **Casos de uso** (aplicação da **lógica de negócio**).
    * `value-objects/`: **Objetos de valor** do domínio (ex: `Email`, `Password`).
* `pkg/`: Pacotes **utilitários** reutilizáveis (ex: **JWT**, **hash**, **email**, **erros**).

## ✨ Principais Características

* **Domain-Driven Design (DDD)**: Uso de **entidades**, **agregados**, **value objects** e **casos de uso**.
* **Injeção de Dependências**: O arquivo `main.go` centraliza a composição dos serviços.
* **Unit of Work**: Gerenciamento explícito de **transações** para operações **atômicas**.
* **Repositórios**: Abstração do acesso a dados, facilitando testes e manutenção.
* **Producers/Consumers de Fila**: Integração **assíncrona** via **RabbitMQ** para tarefas como envio de e-mails.
* **Middlewares**: Autenticação **JWT** e outros controles de acesso.
* **Migrações**: Scripts **SQL** versionados para criação e alteração do **schema** do banco.

## ➡️ Fluxo de Requisição

1.  O **HTTP Handler** recebe a requisição (ex: criação de usuário).
2.  O **DTO** é validado e convertido para parâmetros de **caso de uso**.
3.  O **Use Case** executa a **lógica de negócio**, usando **repositórios**, **unit of work** e outros serviços.
4.  As respostas são padronizadas via `pkg/returns`.
5.  Ocorre a integração com **filas** para tarefas **assíncronas** (ex: envio de e-mail de reset de senha).

## ☁️ Infraestrutura

* **Docker**: Ambiente de desenvolvimento com **Docker Compose** para a **API**, **Postgres**, **RabbitMQ** e **Nginx**.
* **Makefile**: Scripts para **build**, **migração** e **geração de chaves**.
* **Variáveis de ambiente**: Centralizadas em `.env` e validadas em `internal/envs`.
* **GCP**: Hospedado em uma **máquina virtual**.