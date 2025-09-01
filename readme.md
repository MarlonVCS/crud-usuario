# Cadastro de Usuário · CRUD simples com Spring Boot

Pequeno projeto REST para **criar, ler, atualizar e deletar** usuários.Camadas bem definidas (**Controller → Service → Repository → Entity**), persistência com **Spring Data JPA** e banco **H2** em tempo de execução.

> **Stack**: Java 24 · Spring Boot 3.5.5 · Spring Web · Spring Data JPA · H2 · Lombok · Maven

---

## ✨ O que este projeto faz

- **POST** `/usuario` — cria usuário
- **GET** `/usuario?email=` — busca usuário por e-mail
- **PUT** `/usuario?id=` — atualiza nome/e-mail pelo **id**
- **DELETE** `/usuario?email=` — apaga usuário por e-mail

---

## 🧩 Modelo de dados

`Usuario` (exemplo mínimo, com Lombok):

```java
Integer id;
String  nome;
String  email;
```

JSON:

```json
{
  "nome": "Marlon Souza",
  "email": "marlon@exemplo.com"
}
```

---

## ▶️ Como rodar localmente (passo a passo)

### 1) Requisitos

- **JDK 24** (ou compatível com a sua configuração do `pom.xml`)
- **Maven 3.9+** (ou use o wrapper `mvnw`)

### 2)  `application.properties` para H2 em memória

Crie `src/main/resources/application.properties` com o exemplo abaixo caso ainda não exista:

```properties
spring.application.name=crud-usuario

spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
spring.datasource.url=jdbc:h2:mem:usuarios
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

server.port = 8081
```

> Console do H2: `http://localhost:8081/h2-console`
> 
> JDBC URL: `jdbc:h2:mem:usuarios`
> 
>User: `sa` · Password: *(vazio)*

### 3) Subir a aplicação

```bash
./mvnw spring-boot:run
# ou
mvn spring-boot:run
```

A API ficará em `http://localhost:8081`.

---

## 📚 Endpoints e exemplos

### 1) Criar usuário

**POST** `/usuario`
Body:

```json
{
  "nome": "Marlon Souza",
  "email": "marlon.souza@exemplo.com"
}
```

**Resposta**: `200 OK` (sem corpo)



### 2) Buscar por e-mail

**GET** `/usuario?email=marlon.souza@exemplo.com`
**Resposta** `200 OK`:

```json
{
  "id": 1,
  "nome": "Marlon Souza",
  "email": "marlon.souza@exemplo.com"
}
```
---

### 3) Atualizar por **id**

**PUT** `/usuario?id=1`
Body (campos parciais são aceitos; o service preserva os não informados):

```json
{
  "nome": "marlon",
  "email": "marlon.souza@exemplo.com"
}
```

**Resposta**: `200 OK` (sem corpo)


---

### 4) Deletar por e-mail


**DELETE** `/usuario?email=marlon.souza@exemplo.com`

**Resposta**: `200 OK` (sem corpo)



---

## ⚠️ Tratamento de erros (estado atual)

- Quando **e-mail** ou **id** não são encontrados, o Service lança `RuntimeException`.
- Sem um handler global, isso resulta em **HTTP 500** com a mensagem da exceção.

---

## 🛠️ Dependências principais (do `pom.xml`)

- `spring-boot-starter-web`
- `spring-boot-starter-data-jpa`
- `com.h2database:h2` (runtime)
- `org.projectlombok:lombok`

---

