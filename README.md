# Arquitetura de Microserviços com Apache Kafka

Durante o curso **"Arquitetura de Microserviços: Padrão Saga Orquestrado"**, ministrado pelo instrutor **Victor Hugo Negrisoli**, aprendi e implementei uma arquitetura de microserviços utilizando o **Apache Kafka** como meio de comunicação assíncrona entre os serviços. O principal objetivo foi aplicar o padrão **Saga Orquestrado** para garantir consistência em transações distribuídas.

## Microsserviços da Arquitetura

A arquitetura desenvolvida é composta por cinco microsserviços, cada um com responsabilidades bem definidas:

### 1. **Order-Service**
- Responsável por criar o pedido inicial e receber notificações dos outros serviços.  
- Disponibiliza endpoints REST para iniciar o processo e consultar eventos.  
- **Banco de dados**: MongoDB.

### 2. **Orchestrator-Service**
- Centraliza a orquestração do fluxo da Saga, gerenciando o estado e a sequência dos microsserviços envolvidos.  
- Salva o progresso dos eventos e decide qual serviço deve ser chamado a seguir.  
- **Banco de dados**: Não utilizado.

### 3. **Product-Validation-Service**
- Valida se o produto do pedido existe e está em conformidade.  
- Armazena a validação associada ao ID do pedido.  
- **Banco de dados**: PostgreSQL.

### 4. **Payment-Service**
- Calcula e realiza o pagamento com base no pedido, considerando preços unitários e quantidades.  
- Armazena informações de pagamento relacionadas ao ID do pedido.  
- **Banco de dados**: PostgreSQL.

### 5. **Inventory-Service**
- Atualiza o estoque com base nos produtos do pedido.  
- Armazena informações de baixa de estoque relacionadas ao ID do pedido.  
- **Banco de dados**: PostgreSQL.

## Deploy dos Microsserviços
Todos os microsserviços são executados através de um arquivo **docker-compose.yml**, garantindo que a arquitetura seja facilmente configurável e replicável.

---

A implementação proporcionou uma visão prática do uso de Kafka para comunicação entre serviços e da aplicação do padrão Saga para lidar com consistência em arquiteturas distribuídas.
