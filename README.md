# Ecommerce Shopping Microsrvices

<h2>Descrição Geral</h2>
<p>Este projeto é uma implementação passo a passo de uma arquitetura de microsserviços de referência, utilizando tecnologias modernas e padrões amplamente adotados no ecossistema .NET. Ele combina as melhores práticas para construir sistemas escaláveis, modulares e de alto desempenho.</p>

<p>A arquitetura inclui microsserviços desenvolvidos com <strong>ASP.NET Web API</strong>, <strong>Docker</strong>, <strong>RabbitMQ</strong>, <strong>MassTransit</strong>, <strong>gRPC</strong>, <strong>YARP API Gateway</strong>, <strong>PostgreSQL</strong>, <strong>Redis</strong>, <strong>SQLite</strong>, <strong>SQL Server</strong>, <strong>Marten</strong>, <strong>Entity Framework Core</strong>, <strong>CQRS</strong>, <strong>MediatR</strong>, e <strong>DDD</strong>. O projeto também segue os princípios de <strong>Arquitetura Limpa</strong> e <strong>Arquitetura Vertical</strong>, utilizando os recursos mais recentes do <strong>.NET 8</strong> e <strong>C# 12</strong>.</p>

<p>
  Os microsserviços desenvolvidos incluem funcionalidades para um sistema de comércio eletrônico, como:
</p>
<ul>
  <li><strong>Catálogo</strong>: Gerenciamento de produtos.</li>
  <li><strong>Cesta</strong>: Operações de carrinho de compras.</li>
  <li><strong>Desconto</strong>: Aplicação de cupons e promoções.</li>
  <li><strong>Pedidos</strong>: Processamento e gerenciamento de pedidos.</li>
  <li><strong>YARP API Gateway</strong>: Centralização de APIs para comunicação eficiente.</li>
  <li><strong>Shopping.Web</strong>: Aplicação cliente para o consumidor final.</li>
</ul>

<p>Os dados dos microsserviços são armazenados em bancos de dados relacionais e NoSQL, com comunicação entre serviços realizada via <strong>gRPC</strong> e <strong>RabbitMQ</strong> em um modelo orientado a eventos. O <strong>YARP API Gateway</strong> facilita operações do cliente, garantindo uma interface fluida e segura.</p>

<p>Essa arquitetura foi projetada para servir como uma base sólida para projetos de microsserviços complexos, aproveitando tecnologias avançadas para oferecer um equilíbrio entre simplicidade, escalabilidade e desempenho.</p>

<h3>Arquitetura</h3>
<img src="https://github.com/user-attachments/assets/fc42a5c2-21f2-4518-9e27-830deeb85321" style="width:100%;" />



<h2>Catalog Microservice</h2>
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


<h2>Basket Microservice</h2>
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


<h3>Shopping.Web</h3>
<img src="https://github.com/user-attachments/assets/178e5d7b-0209-4c96-9c7c-05028821e0e6" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/d6d89ba5-3b02-413b-b15b-5135008faf13" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/8df7a5ba-dac6-4853-ae88-b31b35b825e9" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/93219288-e6ef-43e7-a8cf-8eb37df5217b" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/29774f7e-6dff-4aed-b712-38c6e74953c3" style="width:33%;" />
<img src="https://github.com/user-attachments/assets/49b5be68-11bf-4004-b82e-bbd7790f3129" style="width:33%;" />

