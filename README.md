## 🔨 O projeto

O Alura Food é uma plataforma fictícia de compra de alimentos, e é o projeto do curso de Microserviços na prática: implementando com Java e Spring na plataforma Alura.
O projeto consiste em 4 microserviços, sendo eles de pagamentos, pedidos, gateway e server. 

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

## 🔨 Objetivos do projeto

- Crie um microsserviço com Java e Spring, conectando a um banco de dados MySQL;
- Implemente a técnica de service discovery utilizando o Eureka;
- Centralize requisições adicionando um API Gateway ao projeto;
- Projete e faça comunicação síncrona entre dois microsserviços com Open Feign;
- Entenda os conceitos de circuit breaker e fallback.

## ⚙️ Funcionalidades do microserviço de pagamentos

- [x] Listar Pagamentos (GET /pagamentos):
Endpoint para listar os pagamentos cadastrados.
Utiliza paginação para retornar os resultados de forma paginada.

- [x] Detalhar Pagamento (GET /pagamentos/{id}):
Endpoint para obter detalhes de um pagamento específico com base no ID fornecido.

- [x] Cadastrar Pagamento (POST /pagamentos):
Endpoint para cadastrar um novo pagamento.
Recebe um payload JSON contendo os dados do pagamento a ser cadastrado.
Retorna o status 201 CREATED com o URI do novo recurso no cabeçalho Location.

- [x] Atualizar Pagamento (PUT /pagamentos/{id}):
Endpoint para atualizar os dados de um pagamento existente com base no ID fornecido.
Recebe um payload JSON contendo os novos dados do pagamento a serem atualizados.
Retorna o status 200 OK com os dados do pagamento atualizados.

- [x] Remover Pagamento (DELETE /pagamentos/{id}):
Endpoint para remover um pagamento existente com base no ID fornecido.
Retorna o status 204 NO CONTENT após a remoção bem-sucedida.

- [x] Confirmar Pagamento (PATCH /pagamentos/{id}/confirmar):
Endpoint para confirmar o pagamento de um pedido com base no ID fornecido.
Utiliza o padrão de Circuit Breaker para tratamento de falhas em chamadas de integração.
No caso de falha na confirmação do pagamento, executa um método de fallback para atualizar o status do pedido.

## ⚙️ Funcionalidades do microserviço de pedidos

- [x] Listagem de Todos os Pedidos:
Endpoint: GET /pedidos
Descrição: Retorna uma lista de todos os pedidos registrados no sistema.

- [x] Buscar Pedido por ID:
Endpoint: GET /pedidos/{id}
Descrição: Permite buscar detalhes de um pedido específico com base no seu ID.

- [x] Obter Porta do Servidor:
Endpoint: GET /pedidos/porta
Descrição: Retorna a porta do servidor onde o serviço está sendo executado.

- [x] Realizar Pedido:
Endpoint: POST /pedidos
Descrição: Permite criar um novo pedido no sistema.

- [x] Atualizar Status do Pedido:
Endpoint: PUT /pedidos/{id}/status
Descrição: Permite atualizar o status de um pedido específico com base no seu ID.

- [x] Aprovar Pagamento do Pedido:
Endpoint: PUT /pedidos/{id}/pago
Descrição: Marca um pedido como pago.















