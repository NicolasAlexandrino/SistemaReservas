# 🏨 Hospeda — Sistema de Gestão de Reservas

Sistema web para gerenciamento de hóspedes, quartos e reservas de hotéis e pousadas, desenvolvido como projeto acadêmico da disciplina de **Desenvolvimento Backend com Spring Boot**.

A aplicação possui uma API REST desenvolvida em Java com Spring Boot, utilizando PostgreSQL para persistência dos dados, Spring Data JPA para mapeamento objeto-relacional e uma interface web integrada para gerenciamento das operações.

## 🎯 Objetivo do projeto

Desenvolver uma aplicação backend que permita administrar as principais operações de um hotel ou pousada, aplicando conceitos de desenvolvimento de APIs REST, arquitetura em camadas, relacionamentos entre entidades, DTOs, validações, tratamento de exceções e regras de negócio.

## 🚀 Funcionalidades

### Gerenciamento de hóspedes
- Cadastrar hóspedes.
- Consultar hóspedes individualmente ou listar todos.
- Atualizar informações dos hóspedes.
- Excluir hóspedes sem reservas vinculadas.
- Pesquisar por nome e e-mail.
- Impedir o cadastro de e-mails duplicados.

### Gerenciamento de quartos
- Cadastrar quartos.
- Consultar quartos individualmente ou listar todos.
- Atualizar informações dos quartos.
- Excluir quartos sem reservas vinculadas.
- Filtrar por tipo, disponibilidade e capacidade mínima.
- Impedir o cadastro de números de quartos duplicados.

### Gerenciamento de reservas
- Criar reservas vinculadas a hóspedes e quartos.
- Consultar reservas individualmente ou listar todas.
- Atualizar reservas existentes.
- Cancelar reservas.
- Excluir reservas.
- Filtrar por status, hóspede, quarto e intervalo de datas.
- Calcular automaticamente o valor total da hospedagem.
- Impedir reservas com datas conflitantes.

## 🛠️ Tecnologias utilizadas

| Tecnologia | Utilização |
|---|---|
| Java 25 | Linguagem de programação |
| Spring Boot 4.1.2 | Framework backend |
| Spring Web MVC | Desenvolvimento da API REST |
| Spring Data JPA | Persistência e consultas ao banco |
| Hibernate | Mapeamento objeto-relacional |
| PostgreSQL | Banco de dados relacional |
| Maven | Gerenciamento de dependências |
| Lombok | Redução de código repetitivo |
| Jakarta Validation | Validação de dados |
| Springdoc OpenAPI | Documentação Swagger |
| JUnit 5 | Testes automatizados |
| Mockito | Simulação de dependências nos testes |
| HTML5 | Estrutura do frontend |
| CSS3 | Estilização da interface |
| JavaScript | Integração com a API |

## 🏗️ Arquitetura do projeto

O projeto utiliza arquitetura em camadas, separando as responsabilidades de cada parte da aplicação.

```text
src/
├── main/
│   ├── java/com/TrabalhoBack/demo/
│   │   ├── config/
│   │   │   └── OpenApiConfig.java
│   │   │
│   │   ├── controller/
│   │   │   ├── HospedeController.java
│   │   │   ├── QuartoController.java
│   │   │   └── ReservaController.java
│   │   │
│   │   ├── dto/
│   │   │   ├── HospedeDTO.java
│   │   │   ├── HospedeRequestDTO.java
│   │   │   ├── QuartoDTO.java
│   │   │   ├── QuartoRequestDTO.java
│   │   │   ├── ReservaDTO.java
│   │   │   └── ReservaRequestDTO.java
│   │   │
│   │   ├── exception/
│   │   │   ├── ApiError.java
│   │   │   ├── BusinessException.java
│   │   │   ├── GlobalExceptionHandler.java
│   │   │   ├── InvalidRequestException.java
│   │   │   └── ResourceNotFoundException.java
│   │   │
│   │   ├── model/
│   │   │   ├── Hospede.java
│   │   │   ├── Quarto.java
│   │   │   └── Reserva.java
│   │   │
│   │   ├── repository/
│   │   │   ├── HospedeRepository.java
│   │   │   ├── QuartoRepository.java
│   │   │   └── ReservaRepository.java
│   │   │
│   │   ├── service/
│   │   │   ├── HospedeService.java
│   │   │   ├── QuartoService.java
│   │   │   └── ReservaService.java
│   │   │
│   │   └── DemoApplication.java
│   │
│   └── resources/
│       ├── application.properties
│       └── static/
│           ├── index.html
│           ├── styles.css
│           └── app.js
│
└── test/
    └── java/com/TrabalhoBack/demo/
        ├── DemoApplicationTests.java
        └── service/
            └── ReservaServiceTest.java
```

### Responsabilidade das camadas

- **Controller:** recebe as requisições HTTP e retorna as respostas da API utilizando ResponseEntity.
- **Service:** concentra as regras de negócio, validações e operações do sistema.
- **Repository:** realiza a comunicação com o banco de dados por meio do Spring Data JPA.
- **Model:** representa as entidades persistidas no banco de dados.
- **DTO:** controla os dados recebidos e retornados pela API.
- **Exception:** centraliza o tratamento de erros e exceções.
- **Config:** contém as configurações da documentação OpenAPI.

## 🗄️ Banco de dados e relacionamentos

O projeto utiliza PostgreSQL e possui três entidades principais:

**Hospede**
- id
- nome
- email
- telefone

**Quarto**
- id
- numero
- tipo
- capacidade
- valorDiaria
- disponivel

**Reserva**
- id
- dataCheckin
- dataCheckout
- quantidadeHospedes
- valorTotal
- status
- hospede_id
- quarto_id

### Relacionamentos JPA

- Um hóspede pode possuir várias reservas (`@OneToMany`).
- Uma reserva pertence a um único hóspede (`@ManyToOne`).
- Um quarto pode possuir várias reservas (`@OneToMany`).
- Uma reserva pertence a um único quarto (`@ManyToOne`).

## ⚙️ Como executar o projeto

### 1. Pré-requisitos

Antes de executar a aplicação, é necessário possuir:

- Java JDK 25.
- PostgreSQL.
- Maven (opcional, pois o projeto possui Maven Wrapper).
- IDE de desenvolvimento, como IntelliJ IDEA, Eclipse ou VS Code.

### 2. Clonar o repositório

```bash
git clone https://github.com/SEU-USUARIO/SEU-REPOSITORIO.git
```

Entre na pasta do projeto:

```bash
cd demo
```

### 3. Configurar o banco de dados

Abra o PostgreSQL pelo pgAdmin e execute:

```sql
CREATE DATABASE "SistemaReserva";
```

### 4. Configurar a conexão

Abra o arquivo:

`src/main/resources/application.properties`

Configure os dados de conexão do PostgreSQL:

```properties
spring.application.name=demo

spring.datasource.url=jdbc:postgresql://localhost:5432/SistemaReserva
spring.datasource.username=postgres
spring.datasource.password=SUA_SENHA

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

Substitua `SUA_SENHA` pela senha configurada no PostgreSQL.

**Importante:** não publique senhas reais no GitHub. Utilize variáveis de ambiente ou uma configuração local protegida para as credenciais do banco.

O Hibernate será responsável por criar e atualizar as tabelas conforme as entidades mapeadas.

### 5. Executar a aplicação

No Windows:

```bash
mvnw.cmd spring-boot:run
```

No Linux ou macOS:

```bash
./mvnw spring-boot:run
```

Após a inicialização, a aplicação estará disponível em:

```text
http://localhost:8080
```

## 📖 Documentação da API — Swagger

A documentação interativa foi implementada utilizando Springdoc OpenAPI.

Acesse:

http://localhost:8080/swagger-ui/index.html

Por meio do Swagger é possível visualizar os endpoints, consultar parâmetros, verificar os modelos de requisição e resposta e executar operações diretamente na documentação.

## 🔗 Endpoints da API

A API possui três recursos principais: hóspedes, quartos e reservas.

### Hóspedes — `/hospedes`

| Método HTTP | Endpoint | Descrição |
|---|---|---|
| GET | `/hospedes` | Lista hóspedes com filtros opcionais |
| GET | `/hospedes/{id}` | Consulta um hóspede |
| POST | `/hospedes` | Cadastra um hóspede |
| PUT | `/hospedes/{id}` | Atualiza um hóspede |
| DELETE | `/hospedes/{id}` | Exclui um hóspede |

Filtros disponíveis:

```text
GET /hospedes?nome=Nicolas
GET /hospedes?email=exemplo@gmail.com
```

### Quartos — `/quartos`

| Método HTTP | Endpoint | Descrição |
|---|---|---|
| GET | `/quartos` | Lista quartos com filtros |
| GET | `/quartos/{id}` | Consulta um quarto |
| POST | `/quartos` | Cadastra um quarto |
| PUT | `/quartos/{id}` | Atualiza um quarto |
| DELETE | `/quartos/{id}` | Exclui um quarto |

Filtros disponíveis:

```text
GET /quartos?tipo=Luxo
GET /quartos?disponivel=true
GET /quartos?capacidadeMinima=2
```

É possível combinar os filtros:

```text
GET /quartos?tipo=Luxo&disponivel=true&capacidadeMinima=2
```

### Reservas — `/reservas`

| Método HTTP | Endpoint | Descrição |
|---|---|---|
| GET | `/reservas` | Lista reservas com filtros |
| GET | `/reservas/{id}` | Consulta uma reserva |
| POST | `/reservas` | Cria uma reserva |
| PUT | `/reservas/{id}` | Atualiza uma reserva |
| PATCH | `/reservas/{id}/cancelamento` | Cancela uma reserva |
| DELETE | `/reservas/{id}` | Exclui uma reserva |

Filtros disponíveis:

```text
GET /reservas?status=CONFIRMADA
GET /reservas?hospedeId=1
GET /reservas?quartoId=2
GET /reservas?dataInicio=2026-12-01&dataFim=2026-12-31
```

Também é possível combinar os filtros:

```text
GET /reservas?status=CONFIRMADA&quartoId=2&dataInicio=2026-12-01&dataFim=2026-12-31
```

## 📝 Exemplos de utilização

### Cadastrar um hóspede

**POST** `/hospedes`

```json
{
  "nome": "Nicolas Alexandrino",
  "email": "nicolas@email.com",
  "telefone": "86999999999"
}
```

### Cadastrar um quarto

**POST** `/quartos`

```json
{
  "numero": 101,
  "tipo": "Luxo",
  "capacidade": 3,
  "valorDiaria": 250.00,
  "disponivel": true
}
```

### Criar uma reserva

**POST** `/reservas`

```json
{
  "dataCheckin": "2026-12-10",
  "dataCheckout": "2026-12-13",
  "quantidadeHospedes": 2,
  "hospedeId": 1,
  "quartoId": 1
}
```

O sistema calcula automaticamente o valor total da hospedagem considerando a quantidade de diárias e o valor da diária do quarto.

**Exemplo:** três diárias de R$ 250,00 resultam em uma reserva de R$ 750,00.

### Cancelar uma reserva

**PATCH** `/reservas/1/cancelamento`

O sistema altera o status da reserva para `CANCELADA`, respeitando as regras de negócio implementadas.

## 📌 Regras de negócio implementadas

1. Não permitir o cadastro de hóspedes com e-mails duplicados.
2. Não permitir números de quartos duplicados.
3. Não permitir reservas em quartos marcados como indisponíveis.
4. Não permitir quantidade de hóspedes superior à capacidade do quarto.
5. Não permitir reservas com check-out anterior ou igual ao check-in.
6. Não permitir reservas com períodos conflitantes para o mesmo quarto.
7. Calcular automaticamente o valor total da reserva.
8. Não permitir alterações em reservas canceladas.
9. Não permitir cancelar reservas já encerradas.
10. Impedir a exclusão de hóspedes e quartos que possuam reservas vinculadas.

## ⚠️ Validação e tratamento de exceções

A aplicação utiliza Jakarta Validation para validar os dados recebidos, com anotações como:

- `@NotBlank`
- `@NotNull`
- `@Email`
- `@Size`
- `@Min`
- `@DecimalMin`

O tratamento de exceções é centralizado por meio de `@RestControllerAdvice` e `@ExceptionHandler`.

### Principais status HTTP utilizados

| Status | Descrição |
|---|---|
| 200 OK | Consulta ou atualização realizada com sucesso |
| 201 Created | Registro criado com sucesso |
| 204 No Content | Exclusão ou cancelamento realizado com sucesso |
| 400 Bad Request | Dados inválidos ou parâmetros incorretos |
| 404 Not Found | Registro não encontrado |
| 409 Conflict | Violação de uma regra de negócio |

## 🖥️ Interface web

O projeto também possui uma interface frontend integrada à API REST, desenvolvida com HTML, CSS e JavaScript.

A interface permite:

- Visualizar um painel geral com informações do sistema.
- Gerenciar hóspedes.
- Gerenciar quartos.
- Cadastrar e consultar reservas.
- Atualizar e excluir registros.
- Cancelar reservas.
- Aplicar filtros de pesquisa.
- Visualizar mensagens de sucesso e erro nas operações.

A interface é disponibilizada pelo próprio Spring Boot, por meio da pasta `src/main/resources/static`.

Acesse:

http://localhost:8080

## 🧪 Testes automatizados

O projeto contém testes automatizados utilizando JUnit 5, Mockito e MockMvc.

Entre os cenários contemplados estão:

- Criação de reservas com cálculo automático do valor total.
- Impedimento de reservas acima da capacidade do quarto.
- Impedimento de reservas com períodos sobrepostos.
- Validação das datas de check-in e check-out.
- Inicialização do contexto da aplicação.
- Disponibilidade da documentação OpenAPI.
- Disponibilidade da interface web e dos recursos JavaScript.
- Consultas com filtros opcionais.

Para executar os testes:

```bash
mvnw.cmd test
```

## 👨‍💻 Considerações finais

O Hospeda foi desenvolvido com o objetivo de aplicar, na prática, os principais conceitos de desenvolvimento backend utilizando Java e Spring Boot.

O projeto demonstra a construção de uma API REST organizada em camadas, integração com banco de dados relacional, relacionamentos com JPA, utilização de DTOs, validações, tratamento centralizado de exceções e implementação de regras de negócio.

Além da API, foi desenvolvida uma interface web integrada para facilitar a utilização e demonstração das funcionalidades do sistema.

---

**Projeto acadêmico — Desenvolvimento Backend com Spring Boot.**
