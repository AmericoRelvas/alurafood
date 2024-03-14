## 🔨 O projeto

O Alura Food é uma plataforma fictícia de compra de alimentos, e é o projeto da Formação Aprofunde em Java com arquitetura de Microsserviços, Spring e RabbitMQ na plataforma Alura.

O projeto consiste em 5 microserviços, sendo eles de pagamentos, pedidos, avaliação, gateway e server. 

Este projeto usa diversas tecnologias e ferramentas como:

**Java 17:** Linguagem de programação back-end.

**Spring Boot:** Para a construção da aplicação Java de maneira rápida e eficiente.

**Spring Data e Hibernate:** Para a integração com o banco de dados MySQL, utilizando JPA para a camada de persistência.

**Maven:** Como gerenciador de dependências, facilitando o processo de construção e execução do projeto.

**MySQL:** Como banco de dados relacional da aplicação.

**Flyway:** Para a migração e versionamento do banco de dados.

**Spring Validation:** Biblioteca do Spring Framework utilizada para validação de dados de entrada na aplicação.

**Spring Web:** Módulo do Spring Framework para desenvolvimento de aplicações web, fornecendo recursos para construção de controladores, tratamento de requisições HTTP, entre outros.

**Lombok:** Biblioteca Java que simplifica a criação de classes Java através da geração automática de métodos como getters, setters e construtores.

**Modelmapper:** Utilizado para mapeamento de objetos entre camadas da aplicação, facilitando a conversão de DTOs (Data Transfer Objects) para entidades de domínio e vice-versa.

**Spring Cloud Starter Netflix Eureka Client:** Integração com o serviço de registro e descoberta de microserviços Eureka, permitindo que os microserviços se registrem no servidor Eureka e descubram uns aos outros.

**Spring Cloud Starter Netflix Eureka Server:** Utilizada para criar e implantar um servidor de registro e descoberta de serviços em uma arquitetura de microsserviços.

**Spring Cloud Starter OpenFeign:** Facilita a comunicação entre microserviços na arquitetura de microsserviços, permitindo declarar interfaces feitas em Java para descrever a comunicação entre serviços.

**Spring Cloud Starter LoadBalancer:** Biblioteca para balanceamento de carga entre instâncias de serviços registradas no servidor Eureka.

**Resilience4j-Spring-Boot3:** Biblioteca para implementação de tolerância a falhas em sistemas distribuídos, incluindo suporte para circuit breaker e fallback.

**Spring Boot Starter AOP:** Permite a implementação de aspectos e orientação a aspectos em aplicações Spring Boot, possibilitando modularizar e reutilizar funcionalidades comuns.

**Spring Boot Starter Actuator:** Fornece funcionalidades para monitoramento e gerenciamento de aplicações Spring Boot em tempo de execução, incluindo endpoints para saúde, métricas, informações de aplicação, entre outros.

**Docker:** Plataforma de software que permite automatizar a implantação e execução de aplicativos dentro de contêineres de software, proporcionando maior portabilidade e eficiência no desenvolvimento, distribuição e execução de software.

**RabbitMQ:** É um dos message brokers open source mais utilizados no mercado, fornecendo uma plataforma robusta e escalável para a troca de mensagens assíncronas entre diferentes partes de um sistema distribuído. Ele facilita a comunicação entre microsserviços, garantindo a confiabilidade e a entrega das mensagens de forma eficiente.


## 🔨 Objetivos do projeto

- Criar um microsserviço com Java e Spring, conectando a um banco de dados MySQL;
- Implementar a técnica de service discovery utilizando o Eureka;
- Centralizar requisições adicionando um API Gateway ao projeto;
- Projetar e fazer comunicação síncrona entre dois microsserviços com Open Feign;
- Entender os conceitos de circuit breaker e fallback;
- Implementar a comunicação assíncrona em seus microsserviços;
- Realizar o tratamento de falhas no consumo de mensagem;
- Criar um cluster para garantir a alta disponibilidade da comunicação.

## ⚙️ Funcionalidades do microserviço de pagamentos

- [x] Listar Pagamentos (GET /pagamentos):
  - Endpoint para listar os pagamentos cadastrados.
  - Utiliza paginação para retornar os resultados de forma paginada.

- [x] Detalhar Pagamento (GET /pagamentos/{id}):
  - Endpoint para obter detalhes de um pagamento específico com base no ID fornecido.

- [x] Cadastrar Pagamento (POST /pagamentos):
  - Endpoint para cadastrar um novo pagamento.
  - Recebe um payload JSON contendo os dados do pagamento a ser cadastrado.
  - Retorna o status 201 CREATED com o URI do novo recurso no cabeçalho Location.
  - Realiza o envio do pagamento para processamento assíncrono via RabbitMQ.

- [x] Atualizar Pagamento (PUT /pagamentos/{id}):
  - Endpoint para atualizar os dados de um pagamento existente com base no ID fornecido.
  - Recebe um payload JSON contendo os novos dados do pagamento a serem atualizados.
  - Retorna o status 200 OK com os dados do pagamento atualizados.

- [x] Remover Pagamento (DELETE /pagamentos/{id}):
  - Endpoint para remover um pagamento existente com base no ID fornecido.
  - Retorna o status 204 NO CONTENT após a remoção bem-sucedida.

- [x] Confirmar Pagamento (PATCH /pagamentos/{id}/confirmar):
  - Endpoint para confirmar o pagamento de um pedido com base no ID fornecido.
  - Utiliza o padrão de Circuit Breaker para tratamento de falhas em chamadas de integração.
  - No caso de falha na confirmação do pagamento, executa um método de fallback para atualizar o status do pedido.
    
## ⚙️ Funcionalidades do microserviço de pedidos

- [x] Listar Todos os Pedidos (GET /pedidos):
  - Endpoint para listar todos os pedidos cadastrados.
  - Retorna uma lista de objetos PedidoDto.

- [x] Listar Pedido por ID (GET /pedidos/{id}):
  - Endpoint para obter detalhes de um pedido específico com base no ID fornecido.
  - Retorna um objeto PedidoDto com os detalhes do pedido.

- [x] Realizar Pedido (POST /pedidos):
  - Endpoint para realizar um novo pedido.
  - Recebe um payload JSON contendo os detalhes do pedido a ser realizado.
  - Retorna o status 201 CREATED com o URI do novo recurso no cabeçalho Location e o objeto PedidoDto no corpo da resposta.

- [x] Atualizar Status do Pedido (PUT /pedidos/{id}/status):
  - Endpoint para atualizar o status de um pedido existente com base no ID fornecido.
  - Recebe um payload JSON contendo o novo status do pedido.
  - Retorna o status 200 OK com o objeto PedidoDto atualizado no corpo da resposta.

- [x] Aprovar Pagamento do Pedido (PUT /pedidos/{id}/pago):
  - Endpoint para aprovar o pagamento de um pedido com base no ID fornecido.
  - Atualiza o status do pedido para indicar que o pagamento foi aprovado.
  - Retorna o status 200 OK após a aprovação do pagamento.

- [x] Processamento de Detalhes de Pagamento (Listener de RabbitMQ):
  - Componente responsável por receber mensagens do RabbitMQ contendo detalhes de pagamentos associados a pedidos.
  - Ao receber uma mensagem, extrai os dados do pagamento e exibe informações relevantes do pedido no console.
  - Utilizado para acompanhar e registrar detalhes dos pagamentos associados aos pedidos.

## ⚙️ Funcionalidades do microserviço de avaliação

- [x] Processamento de Detalhes de Pagamento (Listener de RabbitMQ):
  - Componente responsável por receber mensagens do RabbitMQ contendo detalhes de pagamentos para avaliação.
  - Ao receber uma mensagem, extrai os dados do pagamento e realiza a avaliação.
  - Em caso de pagamento com número "0001", lança uma exceção indicando falha no processamento.
  - Caso contrário, gera uma mensagem de avaliação contendo informações relevantes do pagamento.
  - Exibe detalhes da avaliação no console para fins de monitoramento e logging.

## ⚙️ Microserviço de Gateway

O microserviço de gateway atua como ponto de entrada único para todos os microserviços da aplicação, roteando as solicitações do cliente para os respectivos serviços de destino. Abaixo estão as configurações e funcionalidades principais deste microserviço:

- **Porta do Servidor:** 8082
  - O microserviço de gateway está configurado para escutar as solicitações na porta 8082.

- **Registro no Eureka Server:**
  - Configuração para registrar o microserviço no servidor Eureka, permitindo a descoberta dinâmica de serviços.

- **Nome da Aplicação:**
  - Nome da aplicação definido como "gateway" no servidor Eureka.

- **Spring Cloud Gateway Discovery Locator:**
  - Habilita a descoberta automática de serviços registrados no servidor Eureka.
  - As solicitações recebidas pelo gateway são roteadas dinamicamente para os serviços correspondentes.

## ⚙️ Microserviço de Servidor (Eureka Server)

O microserviço de servidor atua como um registro centralizado para todos os microserviços da aplicação. Abaixo estão as configurações e funcionalidades principais deste microserviço:

- **Porta do Servidor:** 8081
  - O microserviço de servidor é configurado para escutar as solicitações na porta 8081.

- **Nome da Aplicação:**
  - Nome da aplicação definido como "server" no servidor Eureka.

- **Registro no Eureka Server:**
  - Configuração para registrar o microserviço no próprio servidor Eureka.
  - `register-with-eureka` e `fetch-registry` são configurados como `false` para indicar que este servidor não precisa se registrar em outro servidor Eureka nem buscar informações de registro.

- **Endpoint do Eureka Server:**
  - O servidor Eureka é acessível em `http://localhost:8081/eureka`.













