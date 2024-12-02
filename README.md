# Ecommerce Shopping Microsrvices

<h2>Descrição Geral</h2>
<p>Este projeto é uma implementação passo a passo de uma arquitetura de microsserviços de referência, utilizando tecnologias modernas e padrões amplamente adotados no ecossistema .NET. Ele combina as melhores práticas para construir sistemas escaláveis, modulares e de alto desempenho.</p>

<p>A arquitetura inclui microsserviços desenvolvidos com <strong>ASP.NET Web API</strong>, <strong>Docker</strong>, <strong>RabbitMQ</strong>, <strong>MassTransit</strong>, <strong>gRPC</strong>, <strong>YARP API Gateway</strong>, <strong>PostgreSQL</strong>, <strong>Redis</strong>, <strong>SQLite</strong>, <strong>SQL Server</strong>, <strong>Marten</strong>, <strong>Entity Framework Core</strong>, <strong>CQRS</strong>, <strong>MediatR</strong>, e <strong>DDD</strong>. O projeto também segue os princípios de <strong>Arquitetura Limpa</strong> e <strong>Arquitetura Vertical</strong>, utilizando os recursos mais recentes do <strong>.NET 8</strong> e <strong>C# 12</strong>.</p>

<p>Os microsserviços desenvolvidos incluem funcionalidades para um sistema de comércio eletrônico, como:</p>

<ul>
  <li><strong><a href="#catálogo-microservice">Catálogo</a></strong>: Gerenciamento de produtos.</li>
  <li><strong><a href="#cesta-microservice">Cesta</a></strong>: Operações de carrinho de compras.</li>
  <li><strong><a href="#desconto-microservice">Desconto</a></strong>: Aplicação de cupons e promoções.</li>
  <li><strong><a href="#pedidos-microservice">Pedidos</a></strong>: Processamento e gerenciamento de pedidos.</li>
  <li><strong><a href="#yarp-api-gateway">YARP API Gateway</a></strong>: Centralização de APIs para comunicação eficiente.</li>
  <li><strong><a href="#shoppingweb">Shopping.Web</a></strong>: Aplicação cliente para o consumidor final.</li>
</ul>

<p>Os dados dos microsserviços são armazenados em bancos de dados relacionais e NoSQL, com comunicação entre serviços realizada via <strong>gRPC</strong> e <strong>RabbitMQ</strong> em um modelo orientado a eventos. O <strong>YARP API Gateway</strong> facilita operações do cliente, garantindo uma interface fluida e segura.</p>

<p>Essa arquitetura foi projetada para servir como uma base sólida para projetos de microsserviços complexos, aproveitando tecnologias avançadas para oferecer um equilíbrio entre simplicidade, escalabilidade e desempenho.</p>

<h3>Arquitetura</h3>
<img src="https://github.com/user-attachments/assets/fc42a5c2-21f2-4518-9e27-830deeb85321" style="width:100%;" />



## Catalog Microservice
<p>
  O microserviço de Catálogo é responsável pelo gerenciamento dos produtos no sistema de comércio eletrônico, implementado com foco em simplicidade, modularidade e desempenho. Ele utiliza as tecnologias mais recentes do <strong>.NET 8</strong> e <strong>C# 12</strong>, adotando práticas modernas de desenvolvimento.
</p>

<img src="https://github.com/user-attachments/assets/59f4d5aa-0bca-4d6a-bc32-56ff4f7d71dc" style="width:100%;margin:10px" />

<h4>Principais Características</h4>
<strong>APIs Mínimas com ASP.NET Core</strong>: Utiliza APIs mínimas para simplicidade e desempenho, aproveitando ao máximo os novos recursos do .NET8. <br></br/>

<strong>Arquitetura de Fatia Vertical</strong>:
<ul>
  <li>Estruturado com pastas organizadas por recursos.</li>
  <li>Cada recurso encapsula suas funcionalidades em um único arquivo <code>.cs</code>, consolidando classes relacionadas para melhorar a manutenibilidade.</li>
</ul>
    
<strong>CQRS com MediatR</strong>:
<ul>
  <li>Implementa o padrão <strong>CQRS (Command Query Responsibility Segregation)</strong> com a biblioteca <strong>MediatR</strong>.</li>
  <li>Validação no pipeline CQRS usando <strong>FluentValidation</strong>, garantindo que os comandos e consultas sejam validados antes do processamento.</li>
</ul>

<strong>Banco de Dados Documental com Marten</strong>:
<ul>
  <li>Usa a biblioteca <strong>Marten</strong> para transformar o <strong>PostgreSQL</strong> em um banco de dados documental transacional, simplificando o gerenciamento de dados estruturados e não estruturados.</li>
</ul>

<strong>Definição de Endpoint com Carter</strong>:
<ul>
  <li>Usa a biblioteca <strong>Carter</strong> para organizar e definir endpoints de API mínima de maneira eficiente e modular.</li>
</ul>

<strong>Preocupações Transversais</strong>:
<ul>
  <li>Registro de logs centralizado para monitoramento e rastreamento.</li>
  <li>Tratamento global de exceções para fornecer respostas consistentes.</li>
  <li>Verificações de saúde para monitorar a integridade do serviço.</li>
</ul>
    
<strong>Containerização</strong>:
<ul>
  <li>Configurado para execução em ambientes Docker, com suporte a:
    <ul>
      <li><strong>Dockerfile</strong> para o microsserviço.</li>
      <li><strong>docker-compose</strong> para orquestração do microsserviço e do banco de dados PostgreSQL.</li>
    </ul>
  </li>
</ul>

<h4>Fluxo de Trabalho</h4>
<ol>
  <li><strong>Gerenciamento de Produtos</strong>: Permite criar, listar, atualizar e excluir produtos com operações otimizadas.</li>
  <li><strong>Banco de Dados Transacional</strong>: Aproveita o <strong>Marten</strong> para manipular dados como documentos, facilitando a persistência de dados complexos.</li>
  <li><strong>Validação e Controle</strong>: Utiliza <strong>FluentValidation</strong> para garantir que todas as entradas do sistema sejam validadas antes do processamento.</li>
</ol>



## Basket Microservice
<p>O microserviço de Cesta é responsável por gerenciar as operações relacionadas ao carrinho de compras no sistema de comércio eletrônico. Ele é projetado para ser eficiente, modular e escalável, utilizando tecnologias modernas e padrões arquiteturais comprovados.</p>

<img src="https://github.com/user-attachments/assets/338e741e-ab0d-4a8b-88f1-0a508f2afe15" style="width:100%;margin:10px" />

<h4>Principais Características</h4>
<strong>APIs RESTful com ASP.NET 8 Web API</strong>:
<ul>
  <li>Segue os princípios da API REST para implementar operações CRUD no carrinho de compras.</li>
</ul>

<strong>Uso de Redis como Cache Distribuído</strong>:
<ul>
  <li>Utiliza o Redis como cache sobre o banco de dados <code>basketdb</code> para melhorar o desempenho e reduzir a latência.</li>
</ul>
  
<strong>Padrões Arquiteturais</strong>:
<ul>
  <li>Implementa os padrões <strong>Proxy</strong>, <strong>Decorator</strong> e <strong>Cache-aside</strong> para modularidade e eficiência.</li>
</ul>
  
<strong>Integração com o Serviço de Descontos</strong>:
<ul>
  <li>Consome o serviço <strong>Grpc</strong> do microsserviço de Descontos para calcular o preço final dos produtos no carrinho.</li>
</ul>
  
<strong>Publicação de Mensagens com RabbitMQ</strong>:
<ul>
  <li>Publica eventos de checkout do carrinho (BasketCheckout) em filas utilizando <strong>MassTransit</strong> e <strong>RabbitMQ</strong> para comunicação assíncrona.</li>
</ul>
  
<strong>Containerização</strong>:
<ul>
  <li>Configurado para execução em ambientes Docker, com suporte a:
    <ul>
      <li><strong>Dockerfile</strong> para containerização do microsserviço.</li>
      <li><strong>docker-compose</strong> para orquestração do microsserviço, Redis e PostgreSQL.</li>
    </ul>
  </li>
</ul>

<h4>Fluxo de Trabalho</h4>
<ol>
  <li><strong>Gerenciamento do Carrinho</strong>: Permite adicionar, atualizar, listar e remover itens do carrinho com operações CRUD eficientes.</li>
  <li><strong>Integração com o Serviço de Descontos</strong>: Realiza comunicação síncrona via gRPC para aplicar descontos aos produtos.</li>
  <li><strong>Publicação de Eventos</strong>: Publica eventos de checkout do carrinho para processamento posterior nos microsserviços relevantes.</li>
</ol>



## Discount Microservice

<p>O microserviço de Cesta é responsável por gerenciar as operações relacionadas ao carrinho de compras no sistema de comércio eletrônico. Ele é projetado para ser eficiente, modular e escalável, utilizando tecnologias modernas e padrões arquiteturais comprovados.</p>

<img src="https://github.com/user-attachments/assets/6efc9207-da74-4ab8-b015-2665a83862d7" style="width:100%;margin:10px" />

<h4>Principais Características</h4>

<strong>APIs RESTful com ASP.NET 8 Web API</strong>:
<ul>
  <li>Segue os princípios da API REST para implementar operações CRUD no carrinho de compras.</li>
</ul>

<strong>Uso de Redis como Cache Distribuído</strong>:
<ul>
  <li>Utiliza o Redis como cache sobre o banco de dados <code>basketdb</code> para melhorar o desempenho e reduzir a latência.</li>
</ul>

<strong>Padrões Arquiteturais</strong>:
<ul>
  <li>Implementa os padrões <strong>Proxy</strong>, <strong>Decorator</strong> e <strong>Cache-aside</strong> para modularidade e eficiência.</li>
</ul>
  
<strong>Integração com o Serviço de Descontos</strong>:
<ul>
  <li>Consome o serviço <strong>Grpc</strong> do microsserviço de Descontos para calcular o preço final dos produtos no carrinho.</li>
</ul>

<strong>Publicação de Mensagens com RabbitMQ</strong>:
<ul>
  <li>Publica eventos de checkout do carrinho (BasketCheckout) em filas utilizando <strong>MassTransit</strong> e <strong>RabbitMQ</strong> para comunicação assíncrona.</li>
</ul>
  
<strong>Containerização</strong>:
Configurado para execução em ambientes Docker, com suporte a:
<ul>
  <li><strong>Dockerfile</strong> para containerização do microsserviço.</li>
  <li><strong>docker-compose</strong> para orquestração do microsserviço, Redis e PostgreSQL.</li>
</ul>

<h4>Fluxo de Trabalho</h4>
<ol>
  <li><strong>Gerenciamento do Carrinho</strong>: Permite adicionar, atualizar, listar e remover itens do carrinho com operações CRUD eficientes.</li>
  <li><strong>Integração com o Serviço de Descontos</strong>: Realiza comunicação síncrona via gRPC para aplicar descontos aos produtos.</li>
  <li><strong>Publicação de Eventos</strong>: Publica eventos de checkout do carrinho para processamento posterior nos microsserviços relevantes.</li>
</ol>



## Discount Microservice

<p>O microserviço de Pedidos é responsável pelo gerenciamento de pedidos no sistema de comércio eletrônico. Ele é construído com foco em desempenho, escalabilidade e aderência a práticas arquiteturais modernas.</p>

<img src="https://github.com/user-attachments/assets/c360e204-0d8d-43d3-88d8-871330009aa4" style="width:100%;margin:10px" />

<h4>Principais Características</h4>

<strong>APIs Mínimas com ASP.NET Core</strong>:
<ul>
  <li>Implementa APIs HTTP rápidas utilizando endpoints REST totalmente funcionais para operações CRUD.</li>
</ul>

<strong>Design Orientado por Domínio (DDD)</strong>:
<ul>
  <li>Adota o padrão <strong>DDD (Domain-Driven Design)</strong> com separação clara de responsabilidades e modelos de domínio bem definidos.</li>
</ul>

<strong>CQRS e Arquitetura Limpa</strong>:
<ul>
  <li>Integra o padrão <strong>CQRS (Command Query Responsibility Segregation)</strong> para separar leitura e escrita.</li>
  <li>Implementa <strong>Arquitetura Limpa</strong>, promovendo um design modular e escalável.</li>
</ul>

<strong>Princípios SOLID</strong>:
<ul>
  <li>Segue os princípios SOLID para garantir um código limpo, extensível e de fácil manutenção.</li>
  <li>Injeção de dependência para desacoplamento de componentes.</li>
</ul>
  
<strong>Eventos de Domínio e Integração</strong>:
<ul>
  <li>Eleva e manipula eventos de domínio para coordenar estados internos.</li>
  <li>Utiliza eventos de integração para comunicação com outros microsserviços.</li>
</ul>

<strong>Entity Framework Core e SQL Server</strong>:
<ul>
  <li>Utiliza o <strong>Entity Framework Core</strong> com abordagem Code-First, permitindo modelagem baseada em código e geração automática de migrações.</li>
  <li>Configurações otimizadas para SQL Server com alinhamento à <strong>Arquitetura Limpa</strong>.</li>
</ul>
  
<strong>Integração com RabbitMQ</strong>:
<ul>
  <li>Consome eventos da fila <strong>BasketCheckout</strong> publicada pelo microsserviço de Cesta utilizando <strong>MassTransit</strong> e <strong>RabbitMQ</strong>.</li>
</ul>
    
<strong>Containerização</strong>:
<ul>
  <li>Configurado para execução em ambientes Docker, incluindo o banco de dados SQL Server.</li>
</ul>
    
<h4>Fluxo de Trabalho</h4>
<ol>
  <li><strong>Gestão de Pedidos</strong>: Permite criar, consultar, atualizar e cancelar pedidos.</li>
  <li><strong>Integração com Microsserviços</strong>: Consome eventos de checkout da cesta para iniciar o processamento de pedidos.</li>
  <li><strong>Persistência de Dados</strong>: Utiliza SQL Server para armazenar e gerenciar dados transacionais.</li>
  <li><strong>Manuseio de Eventos</strong>: Eleva eventos de domínio e processa eventos de integração para sincronização com outros microsserviços.</li>
</ol>



## Comunicação Assíncrona de Microsserviços com RabbitMQ e MassTransit

<p>Esta seção descreve a implementação de comunicação assíncrona entre microsserviços utilizando o RabbitMQ como message-broker e o MassTransit como uma abstração para simplificar a interação com o RabbitMQ. Essa abordagem garante a desacoplagem dos microsserviços melhora a escalabilidade do sistema.</p>

<img src="https://github.com/user-attachments/assets/46529411-a240-44ac-bc4d-153a64cec325" style="width:100%;margin:10px" />

<h4>Principais Características</h4>

<strong>RabbitMQ como Message-Broker</strong>:
<ul>
  <li>Configurado como um serviço de mensagens central para comunicação assíncrona entre microsserviços.</li>
  <li>Utiliza o modelo de troca de tópicos (<strong>pub/sub</strong>) para publicação e assinatura de eventos.</li>
</ul>
  
<strong>MassTransit para Abstração</strong>:
<ul>
  <li>Simplifica o uso do RabbitMQ ao fornecer uma abstração sobre o message-broker.</li>
  <li>Facilita a criação e o consumo de mensagens com suporte a middlewares e práticas modernas.</li>
</ul>
  
<strong>Publicação e Consumo de Eventos</strong>:
<ul>
  <li>Publicação do evento <strong>BasketCheckout</strong> no microsserviço de Cesta.</li>
  <li>Assinatura do evento <strong>BasketCheckout</strong> no microsserviço de Pedidos para iniciar o processamento do pedido.</li>
</ul>
  
<strong>RabbitMQ EventBus.Messages</strong>:
<ul>
  <li>Biblioteca compartilhada para definir mensagens de evento e facilitar o compartilhamento de contratos entre microsserviços.</li>
  <li>Referenciada pelos microsserviços de Cesta e Pedidos.</li>
</ul>
  
<strong>Containerização com Docker</strong>:
<li>Configuração do RabbitMQ como serviço em contêiner com suporte a:
  <ul>
    <li>Microsserviço de Cesta.</li>
    <li>Microsserviço de Pedidos.</li>
  </ul>
</li>
<li>Uso do Docker Compose para orquestração.</li>

<h4>Fluxo de Trabalho</h4>
<ol>
  <li><strong>Publicação de Eventos</strong>: O microsserviço de Cesta publica eventos <strong>BasketCheckout</strong> na fila do RabbitMQ.</li>
  <li><strong>Consumo de Eventos</strong>: O microsserviço de Pedidos assina o evento <strong>BasketCheckout</strong> e processa os dados do pedido.</li>
  <li><strong>Integração Simplificada</strong>: O MassTransit gerencia a comunicação, reduzindo a complexidade do código.</li>
</ol>



## Microserviço YarpApiGateway

<p>O <strong>YarpApiGateway</strong> é responsável por centralizar as chamadas dos clientes e roteá-las para os microsserviços apropriados, implementando o padrão de roteamento de gateway. Ele utiliza o <strong>YARP (Yet Another Reverse Proxy)</strong> para configurar e gerenciar o proxy reverso, oferecendo recursos avançados como roteamento dinâmico, transformação de requisições e limitação de taxa.</p>

<img src="https://github.com/user-attachments/assets/d743e190-7cda-4cc7-a536-128314e10c10" style="width:100%;margin:10px" />

<h4>Principais Características</h4>

<strong>API Gateway com YARP</strong>:
<ul>
  <li>Implementa o padrão de <strong>Gateway Routing</strong> para conectar clientes aos microsserviços.</li>
  <li>Centraliza a comunicação e simplifica a integração com os microsserviços.</li>
</ul>
  
<strong>Configuração de Proxy Reverso com YARP</strong>:
<ul>
  <li>Configurações para <strong>Rota</strong>, <strong>Cluster</strong>, <strong>Caminho</strong>, <strong>Transformação</strong> e <strong>Destinos</strong>.</li>
  <li>Flexibilidade para adaptar o roteamento com base nas necessidades do sistema.</li>
</ul>
    
<strong>Limitação de Taxa</strong>:
<ul>
  <li>Implementa <strong>FixedWindowLimiter</strong> para limitar a taxa de requisições ao gateway, protegendo os serviços de sobrecarga.</li>
</ul>
  
<strong>Containerização com Docker Compose</strong>:
<ul>
  <li>Configuração completa para execução em contêiner, facilitando a implantação junto aos microsserviços.</li>
</ul>

<h4>Fluxo de Trabalho</h4>
<ol>
  <li><strong>Recebimento de Requisições</strong>: Recebe todas as chamadas dos clientes no gateway.</li>
  <li><strong>Roteamento e Transformação</strong>: Roteia as requisições para os microsserviços apropriados com base nas configurações. Aplica transformações às requisições para atender aos requisitos dos serviços de destino.</li>
  <li><strong>Gerenciamento de Limitação de Taxa</strong>: Restringe o número de requisições permitidas em um intervalo de tempo usando o FixedWindowLimiter.</li>
  <li><strong>Entrega aos Microsserviços</strong>: Encaminha as requisições aos serviços de destino configurados no cluster.</li>
</ol>



## Aplicativo de Cliente da Web de Compras

<p>O <strong>Aplicativo de Cliente da Web de Compras</strong> é uma interface web que permite aos usuários interagir com o sistema de comércio eletrônico. Ele é desenvolvido com <strong>ASP.NET Core Razor Pages</strong> e utiliza o <strong>Bootstrap 4</strong> para fornecer uma interface moderna, responsiva e amigável ao usuário.</p>

<img src="https://github.com/user-attachments/assets/7e11ef78-683b-4020-8519-03aabc2a882f" style="width:100%;margin:10px" />

<h4>Principais Características</h4>
<strong>ASP.NET Core Razor com Bootstrap 4</strong>:
<ul>
  <li>Desenvolvido com <strong>Razor Pages</strong> para criar páginas dinâmicas e reutilizáveis.</li>
  <li>Utiliza o tema <strong>Bootstrap 4</strong> para garantir um design responsivo e moderno.</li>
</ul>
  
  
<strong>Consumo de APIs via YARP API Gateway</strong>:
<ul>
  <li>Consome as APIs dos microsserviços por meio do <strong>YarpApiGateway</strong>.</li>
  <li>Implementado com a biblioteca <strong>Refit</strong> e <strong>HttpClientFactory</strong> para chamadas HTTP eficientes e reutilizáveis.</li>
</ul>
  
<strong>Recursos do ASP.NET Core Razor</strong>:
<ul>
  <li>Inclui ferramentas como:</li>
  <ul>
    <li><strong>Componentes de exibição</strong>.</li>
    <li><strong>Exibições parciais</strong>.</li>
    <li><strong>Auxiliares de tags</strong>.</li>
    <li><strong>Vinculação e validação de modelos</strong>.</li>
    <li><strong>Seções do Razor</strong> para modularidade e flexibilidade.</li>
  </ul>
</ul>
    
<strong>Containerização com Docker Compose</strong>:
<ul>
  <li>Configurado para ser executado em ambientes Docker, garantindo fácil implantação e escalabilidade.</li>
</ul>

<h4>Fluxo de Trabalho</h4>
<ol>
  <li><strong>Interface de Usuário</strong>: Proporciona uma experiência de usuário amigável com navegação intuitiva.</li>
  <li><strong>Consumo de APIs</strong>: Integra-se perfeitamente com o YarpApiGateway para realizar operações como exibir produtos, gerenciar carrinhos e processar pedidos.</li>
  <li><strong>Validação e Interatividade</strong>: Utiliza recursos do Razor para validações no cliente e servidor, garantindo consistência nos dados.</li>
</ol>

<h4>Interface</h4>
<img src="https://github.com/user-attachments/assets/178e5d7b-0209-4c96-9c7c-05028821e0e6" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/d6d89ba5-3b02-413b-b15b-5135008faf13" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/8df7a5ba-dac6-4853-ae88-b31b35b825e9" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/93219288-e6ef-43e7-a8cf-8eb37df5217b" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/29774f7e-6dff-4aed-b712-38c6e74953c3" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/49b5be68-11bf-4004-b82e-bbd7790f3129" style="width:33%;" />

