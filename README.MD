# Sistema de Gerenciamento de Estacionamento

Este projeto é uma API Rest desenvolvida em **Spring Boot** para gerenciamento de um estacionamento. O sistema inclui autenticação via **JSON Web Token (JWT)**, auditoria, e documentação dos endpoints.

---

## Requisitos do Sistema

### Configurações
- Configuração do **Timezone** e **Locale** para o Brasil.
- Sistema de auditoria:
  - Registro de data de criação e última modificação dos registros.
  - Registro do usuário responsável pela criação ou modificação.
- Conexão com banco de dados no ambiente de desenvolvimento.

### Usuários
- Campos obrigatórios:
  - **E-mail**: único, usado como nome de usuário.
  - **Senha**: no mínimo 6 caracteres.
  - **Perfil**: administrador ou cliente.
- Funcionalidades:
  - Criação de usuários sem autenticação.
  - Recuperação de dados:
    - **Administrador**: pode acessar qualquer usuário.
    - **Cliente**: pode acessar apenas seus próprios dados.
  - Alteração de senha pelo próprio usuário autenticado.
  - Listagem de todos os usuários (restrito a administradores).
- **Testes de integração** (end-to-end) para todos os recursos.

### Autenticação
- Implementação de segurança com **JWT**.
- Documentação completa do sistema de autenticação.
- Testes para validação de autenticação.

### Clientes
- Vinculação obrigatória de um cliente a um usuário.
- Campos obrigatórios:
  - **Nome completo**.
  - **CPF**: único.
- Funcionalidades:
  - **Cliente autenticado**:
    - Recuperar seus próprios dados.
    - Gerar relatórios em PDF com a lista de estacionamentos.
  - **Administrador autenticado**:
    - Listar todos os clientes.
- **Testes de integração** (end-to-end) para os recursos.

### Vagas
- Gerenciamento restrito a administradores:
  - Cada vaga possui um **código único** (diferente do ID).
  - Status da vaga: **livre** ou **ocupada**.
- **Testes de integração** (end-to-end) para as operações.

### Estacionamentos
- Controle das entradas e saídas de veículos.
- Regras de uso:
  - Apenas clientes cadastrados podem estacionar.
  - Registro de informações do veículo e do cliente.
  - Geração de **recibo único** para cada entrada.
  - Controle de **descontos**:
    - 30% de desconto após 10 estacionamentos completos.
- Cálculo do custo:
  - **Primeiros 15 minutos**: R$ 5,00.
  - **Primeira hora completa (60 minutos)**: R$ 9,25.
  - **A cada 15 minutos adicionais**: R$ 1,75.
- **Testes de integração** (end-to-end) para todos os recursos.

---

## Tecnologias Utilizadas
- **Java 17** ![Java](https://img.shields.io/badge/Java-17-007396?logo=java)
- **Spring Boot** ![Spring Boot](https://img.shields.io/badge/Spring%20Boot-2.5.4-6DB33F?logo=spring-boot)
- **Lombok** ![Lombok](https://img.shields.io/badge/Lombok-1.18.20-FF6347?logo=lombok)
- **Swagger** ![Swagger](https://img.shields.io/badge/Swagger-3.0-85EA2D?logo=swagger)
- **H2 Database** ![H2](https://img.shields.io/badge/H2-1.4.200-003545?logo=h2)
- **JWT** ![JWT](https://img.shields.io/badge/JWT-0.9.1-000000?logo=json-web-tokens)
- **IntelliJ IDEA** ![IntelliJ IDEA](https://img.shields.io/badge/IntelliJ%20IDEA-2021.2-000000?logo=intellij-idea)

---

## Instalação e Execução

```bash
# Passo 1: Clone este repositório
$ git clone https://github.com/JoaomBRosio/sistema-completo-de-estacionamento.git

# Passo 2: Acesse o diretório do projeto
$ cd sistema-estacionamento

# Passo 3: Compile e execute a aplicação
$ ./mvnw spring-boot:run

# Passo 4: Acesse a documentação da API
Acesse: http://localhost:8080/swagger-ui/index.html

# Passo 5: Configure o banco de dados no arquivo application.properties, se necessário
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

# Passo 6: Execute os testes para validar o funcionamento
$ ./mvnw test
```

---

## Testes
- Este projeto possui **100% de cobertura de testes unitários**.
- Inclui **testes de integração** (end-to-end) para validar os endpoints implementados.
---

## Autor
Projeto desenvolvido como parte do aprendizado em **Spring Boot** e APIs RESTful - João Ambrósio.
