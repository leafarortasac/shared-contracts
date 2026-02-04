Shared Contracts 📦

   Este projeto é uma biblioteca centralizada de contratos (DTOs e Interfaces) utilizada pelos microsserviços do ecossistema de pedidos. Ele utiliza OpenAPI Generator para garantir que todos os serviços falem a mesma língua através de especificações YAML.

🚀 Tecnologias
   
   Java 21
   Spring Boot 3.4.1
   OpenAPI Generator (Maven Plugin)
   Lombok

🏗️ Estrutura de Contratos
   
   Os contratos são definidos usando o padrão OpenAPI 3.0 na pasta: src/main/resources/swagger/

      pedido-api.yaml: Definições para o fluxo de entrada (Ingestão).

      order-api.yaml: Definições para o fluxo de processamento e saída (Worker).

🛠️ Como Gerar e Instalar
   
   Como esta é uma biblioteca compartilhada, você precisa compilá-la e instalá-la no seu repositório local do Maven (.m2) para que o pedido-service e o order-service consigam importar a dependência.

   1. Limpar e Gerar Código
      Este comando executa o plugin do OpenAPI e gera as classes Java em target/generated-sources.

      Bash
         mvn clean compile
   2. Instalar Localmente
      Este comando torna a biblioteca disponível para outros projetos na sua máquina.

      Bash
         mvn install
📦 Como usar em outras APIs
   
   Adicione a dependência no pom.xml dos seus microsserviços:

   XML
      <dependency>
      <groupId>com.br.shared</groupId>
      <artifactId>shared-contracts</artifactId>
      <version>1.0.0-SNAPSHOT</version>
      </dependency>

📝 Notas de Implementação
   
   Sufixo de Modelos: Todas as classes geradas possuem o sufixo Representation (ex: PedidoRepresentation, OrderRepresentation).

      Tipagem de Data: A biblioteca está configurada para mapear campos de data/hora diretamente para java.time.LocalDateTime.

      Imutabilidade: Os modelos são gerados com suporte a Bean Validation e anotações Jackson para garantir a correta serialização via RabbitMQ.
