A palestra **"AI Gateways: mais segurança e maior governança em suas soluções de Inteligência Artificial!"** foi apresentada no evento TDC SP por **Renato Groffe** (Microsoft MVP, Docker Captain) e **Carlos Machel** (Microsoft MVP, Lead Software Developer na Azure Brasil).

### Principais Pontos da Palestra

- **O que é um AI Gateway**: É um **ponto centralizado de acesso aos modelos de IA** que abstrai o gerenciamento de APIs, centraliza chamadas para múltiplos provedores e aplica políticas de acesso e segurança antes do envio das requisições.
- **Recursos de Segurança**:
  - Autenticação e autorização centralizadas com controle por aplicação/usuário.
  - _Rate limiting_ e proteção contra abusos.
  - Gerenciamento seguro de credenciais e **filtros/guardrails** para requisições e respostas.
- **Governança e FinOps**:
  - Estabelecimento de políticas de uso e limites de consumo (tokens e requisições).
  - Controle de modelos/provedores autorizados.
  - Auditoria, rastreabilidade de chamadas e **acompanhamento de custos**.
- **Padrões de Arquitetura e Alternativas de Mercado**:
  - Apresentação do padrão **Unified AI Gateway** (autenticação unificada, roteamento inteligente, _circuit breaker_ e observabilidade).
  - Alternativas do ecossistema: **APISIX**, **Azure API Management (APIM)**, **Azure AI Gateway**, **Kong** e **LiteLLM**.
  - Funcionalidades avançadas destacadas no APISIX, incluindo suporte a RAG, engenharia de prompts, _caching_, e balanceamento de carga entre múltiplas LLMs.
- **Iniciativas OWASP para IA**: Destaque para as diretrizes de segurança **OWASP Top 10 for LLM Applications 2026**, **OWASP Top 10 for Agentic Applications 2026** e **OWASP MCP Top 10**.
- **Exemplos Práticos**: Apresentação de demonstrações práticas, com código e materiais disponibilizados no repositório GitHub mantido pelos palestrantes (`github.com/renatogroffe/ai-gateways_tdc-sp-2026-09`).
