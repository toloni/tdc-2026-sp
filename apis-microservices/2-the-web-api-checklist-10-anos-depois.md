A palestra **"The Web API Checklist: Designing Resilient and Predictable Contracts"**, apresentada no **The Developer's Conference (TDC)**, faz uma análise sobre a evolução do design de APIs a partir do checklist de 43 itens publicado originalmente por Mathieu Fenniak em 2013. O conteúdo conecta os fundamentos históricos às práticas e padrões modernos da Web.

https://mathieu.fenniak.net/the-api-checklist/

---

### 1. O Conceito de Contrato Amplo

- A API é tratada como um **contrato amplo** que vai muito além do endpoint visível, dependendo do transporte HTTP, servidor, framework e regras de negócio.
- O checklist organiza a experiência da API em três pilares essenciais: **Semântica** (métodos, status, cache, conteúdo), **Produto** (intenção, paginação, versões, documentação) e **Operação** (segurança, throttling, logs, testes).
- O checklist original agrupava 43 itens em 5 tópicos principais: HTTP, API Design, Conteúdo, Segurança e Cliente.

---

### 2. Evolução do HTTP e Transição para Nuvem

- **Timeline do HTTP**: A infraestrutura evoluiu do HTTP/1.1 com TLS opcional em 2013 para o HTTP/2 com multiplexação e TLS 1.3 (2015–2018), chegando ao HTTP/3 com protocolo QUIC e a consolidação da RFC 9110 (2022–2025).
- **On-Premises vs. Cloud**: Em 2013, o foco estava na configuração manual de conexões, SSL e documentação no código; na era Cloud e OpenAPI, a infraestrutura gerencia os mecanismos padrão (TLS, HTTP/2 e HTTP/3), permitindo que os desenvolvedores foquem na governança, no produto e na telemetria.

---

### 3. Previsibilidade e o Princípio da Menor Surpresa (POLA)

- O contrato estabelece uma promessa de **previsibilidade** ao consumidor.
- Métodos HTTP (GET, POST, PUT, PATCH, DELETE), códigos de status (1xx a 5xx) e mecanismos de cache (como `Cache-Control`, `ETag` e `If-None-Match`) definem o que pode ser desenhado, executado e armazenado.
- O **Princípio da Menor Surpresa (POLA)** exige que os nomes antecipem seus efeitos reais, convenções reduzam a curva de aprendizado e regras de tratamento de erros, datas, nulos e paginação sejam consistentes.
- A palestra contrasta o **Design por Intenção** (focado no caso de uso, regras e invariantes) com a **Menor Surpresa** (alinhada ao repertório semântico e expectativas do consumidor).

---

### 4. Quatro Decisões Essenciais de Contrato

Para evitar falhas graves no ambiente de produção, a palestra destaca quatro decisões de contrato cruciais:

1. **Idempotência Real**: Garante que tentativas de reenvio (_retries_) não dupliquem pagamentos, pedidos ou mensagens.
2. **Controle Otimista**: Uso de `ETag` e `If-Match` para detectar conflitos de concorrência antes de sobrescrever dados.
3. **Paginação Estável**: Uso de cursores e ordenação determinística para evitar itens duplicados ou omissões.
4. **Timezone e Unicode**: Definição explícita de fuso horário via RFC 3339 e testes com caracteres especiais.

---

### 5. Segurança Granular e Gestão Útil de Erros

- **Segurança por Efeito**: O canal seguro (HTTPS/TLS) tornou-se o padrão mínimo; os riscos atuais envolvem autorização no nível de objeto e campo, limites de automação em fluxos de negócio e governança do ecossistema.
- **Falhas Úteis**: Respostas opacas transferem complexidade ao cliente. O contrato deve padronizar mensagens de erro usando formatos como _Problem Details_, respostas `429` com header `Retry-After`, validações `400/422` consistentes, IDs de correlação e retries apenas quando seguros.

---

### 6. Contratos Executáveis e Estilos de Arquitetura

- **OpenAPI 3.2**: Permite tratar o contrato como executável para revisar schemas antes do código, automatizar documentação, gerar clientes/mocks e aplicar testes de contrato no pipeline CI/CD.
- **Seleção do Estilo de API**: O estilo deve seguir a necessidade de interação do sistema:
  - **REST**: Recomendado para recursos e APIs públicas/CRUD com semântica HTTP.
  - **GraphQL**: Indicado para telas agregadoras e consultas flexíveis em grafos.
  - **gRPC**: Ideal para comunicação eficiente e fortemente tipada entre microsserviços.
  - **Eventos**: Voltado para processamento assíncrono e desacoplado.

Em suma, a palestra transmite a mensagem de que, como a infraestrutura moderna já resolve a mecânica de transporte[4], o papel principal do desenvolvedor hoje é garantir a **governança do contrato, a previsibilidade do sistema e o valor entregue ao consumidor**
