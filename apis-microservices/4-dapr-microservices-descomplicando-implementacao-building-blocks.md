A palestra **"Dapr: Distributed Application Runtime Overview and Building Blocks"**, apresentada no evento **The Developer's Conference (TDC)**, aborda como o framework Dapr simplifica a criação de microserviços e aplicações distribuídas.

---

### 1. Desafios de Microserviços e Aplicações Distribuídas

A apresentação inicia contextualizando as dificuldades comuns enfrentadas pelos times de desenvolvimento:

- **Complexidade e Falta de Padronização**: Alta complexidade de infraestrutura, diversidade de tecnologias empregadas no mesmo contexto e cada equipe resolvendo problemas à sua maneira.
- **Requisitos Transversais**: Dificuldades constantes com resiliência, observabilidade, segurança e testes de projetos.
- **Foco no Negócio**: Embora a tecnologia seja fundamental, o objetivo primário deve ser atender às necessidades do negócio.

---

### 2. Visão Geral e Arquitetura do Dapr

- **O que é**: Um **Distributed Application Runtime** open-source e multiplataforma, graduado pela **CNCF (Cloud Native Computing Foundation)** desde outubro de 2024.
- **Arquitetura Sidecar**: Os _building blocks_ do Dapr são agrupados em um processo _sidecar_ para a aplicação. A comunicação ocorre via **gRPC** ou **HTTP**, com configurações estruturadas em arquivos **YAML** e gerenciadas via **Dapr CLI**.
- **Ambientes de Implantação**: Funciona em **Kubernetes**, máquinas virtuais (_self-hosted_), ambientes _multi-cloud_, _on-premise_ e serviços _serverless_ como Azure Container Apps e Azure Functions.
- **Recursos de Plataforma**:
  - **Resiliência**: Transfere a resiliência do código-fonte para as configurações da infraestrutura.
  - **Isolamento e Segurança**: Suporte a _namespaces_, facilidade na criação de soluções _multi-tenant_ e políticas de acesso customizáveis na comunicação entre aplicações.
  - **Observabilidade**: Integração nativa com **OpenTelemetry**.

---

### 3. Building Blocks vs. Componentes

O Dapr abstrai a infraestrutura separando o conceito de **Building Blocks** (APIs funcionais expostas para a aplicação) e **Componentes** (tecnologias concretas de infraestrutura):

- **State Management**: Gerenciamento de estado com suporte a componentes como Redis e PostgreSQL.
- **Publish / Subscribe**: Mensageria escalável e segura utilizando RabbitMQ, Azure Service Bus, Kafka, entre outros.
- **Bindings**: Integrações de entrada/saída com recursos externos como Azure Blob Storage e Amazon S3.
- **Secrets**: Acesso seguro a segredos armazenados em cofres como Azure Key Vault, HashiCorp Vault e OpenBao.
- **Conversation (IAs Generativas)**: Abstração para comunicação com modelos de IA como OpenAI, Anthropic e Google.
- **Outros Módulos**: Inclui _Service Invocation_, _Workflow_, _Actors_, _Configuration_, _Distributed Lock_, _Cryptography_, _Jobs_ e _Middleware_.

---

### 4. Principais Benefícios

- **Foco no Negócio e Produtividade**: Permite que os desenvolvedores foquem na regra de negócio em vez de implementarem detalhes técnicos de infraestrutura.
- **Multi-Stack**: Suporta diversas linguagens e plataformas (.NET, Java, Python, JavaScript/Node.js, Go, PHP, C++, Rust), oferecendo padronização para times heterogêneos.
- **Integração Agnóstica**: Facilita a troca de provedores de infraestrutura sem impactar o código e serve como alternativa robusta para o desenvolvimento de produtos **SaaS (Software as a Service)**.

---
