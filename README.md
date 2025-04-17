# 📦 Microsserviço em Java com Spring Boot

Este projeto é um microsserviço desenvolvido em Java utilizando o framework Spring Boot, com foco em comunicação assíncrona via mensageria, persistência de dados, validações, envio de e-mails e uma arquitetura limpa e escalável.

## 🧰 Tecnologias e Dependências Utilizadas

### Spring Boot
- `spring-boot-starter-web` – Criação de APIs REST
- `spring-boot-starter-data-jpa` – Integração com banco de dados via JPA/Hibernate
- `spring-boot-starter-validation` – Validações automáticas com Bean Validation
- `spring-boot-starter-amqp` – Integração com mensageria (RabbitMQ)
- `spring-boot-starter-mail` – Envio de e-mails

### Banco de Dados
- **PostgreSQL** – Utilizado como sistema gerenciador de banco de dados relacional (SGBD)

### Mensageria
- RabbitMQ como broker de mensagens
- CloudAMQP como serviço hospedado de RabbitMQ

### E-mail
- SMTP Gmail para envio de e-mails transacionais

## 🧱 Arquitetura

O sistema segue uma arquitetura baseada em microsserviços, com uso de mensageria para desacoplamento de responsabilidades. A comunicação entre partes do sistema ocorre através de mensagens assíncronas utilizando RabbitMQ, o que melhora a escalabilidade e tolerância a falhas.

## 🐇 O que é RabbitMQ?

RabbitMQ é um broker de mensagens que atua como um intermediário entre diferentes partes de um sistema. Ele permite que aplicações enviem e recebam mensagens de forma assíncrona por meio de filas (queues).

**No contexto do projeto:**
- O microsserviço publica mensagens em uma fila (ex: notificação por e-mail ou criação de registro)
- Outro serviço (ou o mesmo) consome mensagens dessa fila para realizar uma ação, como o envio de e-mail
- Isso garante que a operação aconteça mesmo que o serviço de envio de e-mails esteja temporariamente indisponível

## ☁️ O que é CloudAMQP?

CloudAMQP é um serviço de hospedagem de RabbitMQ na nuvem, permitindo usar a mensageria sem precisar instalar e configurar um servidor RabbitMQ localmente.

**Vantagens:**
- Alta disponibilidade e escalabilidade
- Acesso remoto com login/senha e URL AMQP
- Dashboard para monitoramento em tempo real

## 📬 Envio de E-mails com SMTP Gmail

SMTP (Simple Mail Transfer Protocol) é um protocolo padrão para envio de e-mails. O Gmail disponibiliza um servidor SMTP para permitir que aplicativos enviem e-mails usando uma conta Google.

**Como foi utilizado:**
- Foi criada (ou utilizada) uma conta Gmail dedicada para o envio de e-mails.
- Foi ativado o Acesso a apps menos seguros (ou criado uma senha de app, caso com autenticação em dois fatores).
- Configurações adicionadas no application.properties:

### Spring Boot
`spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=seuemail@gmail.com
spring.mail.password=sua-senha-ou-senha-de-app
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true`

- A classe JavaMailSender foi utilizada para enviar e-mails com texto ou HTML.

## 🗃️ Banco de Dados

Foi utilizado PostgreSQL como banco de dados relacional. As entidades são mapeadas via JPA, com uso de repositórios (JpaRepository) para persistência e consulta dos dados.

## 🧪 Funcionalidades do Microsserviço

- Exposição de endpoints REST com validação
- Persistência de dados com PostgreSQL
- Envio assíncrono de e-mails usando filas do RabbitMQ
- Integração com CloudAMQP
- Envio real de e-mails com SMTP Gmail
- Tratamento de exceções e logs
