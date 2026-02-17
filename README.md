Shared Contracts 📦

Este projeto é uma biblioteca centralizada de contratos (DTOs e Interfaces) utilizada por todos os microsserviços do ecossistema. Ele utiliza o OpenAPI Generator para garantir que o Mobile, o Frontend e os Microsserviços falem a mesma língua através de especificações YAML rigorosas.

🚀 Tecnologias

Java 21

Spring Boot 3.4.1

OpenAPI Generator (Maven Plugin): Geração automática de código.

Lombok: Redução de boilerplate.

🏗️ Estrutura de Contratos

Os contratos são definidos usando o padrão OpenAPI 3.0 na pasta: src/main/resources/swagger/. Cada YAML representa o contrato de um domínio específico do ecossistema:

    iam-api.yaml: Autenticação, Perfis e Tokens.
    task-api.yaml: Regras de negócio de Gerenciamento de Tarefas.
    notification-api.yaml: Estrutura de mensagens para Filas e MQTT.
    pedido-api.yaml & order-api.yaml: Contratos para integração de fluxos de ordens.

🛠️ Como Gerar e Instalar
Como esta é uma biblioteca compartilhada, você precisa compilá-la e instalá-la no seu repositório local do Maven (.m2) para que os demais serviços consigam importar a dependência durante o build no Docker.

1. Limpar e Gerar Código
   Este comando executa o plugin do OpenAPI e gera as classes Java em target/generated-sources.

Bash
mvn clean compile

2. Instalar Localmente
   Este comando torna a biblioteca disponível para os outros projetos na sua máquina e para o processo de build do Docker.

Bash
mvn install
📦 Como usar em outras APIs
Adicione a dependência no pom.xml dos microsserviços (iam-api, task-api, notification-api, etc.):

    XML
    <dependency>
    <groupId>com.br.shared</groupId>
    <artifactId>shared-contracts</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    </dependency>

📝 Notas de Implementação

Sufixo de Modelos: Todas as classes geradas possuem o sufixo Representation (ex: TaskRepresentation, UsuarioRepresentation) para evitar conflitos com entidades de persistência.

      Tipagem de Data: Configurada para java.time.LocalDateTime para garantir precisão nos filtros por data.

      Contratos Universais: A mesma biblioteca é utilizada para gerar os tipos no backend e servir de referência para o Swagger consumido pelo Frontend e Mobile.