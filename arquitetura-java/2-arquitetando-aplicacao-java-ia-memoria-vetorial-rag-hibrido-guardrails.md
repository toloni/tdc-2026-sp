A palestra **"Architecting an Intelligent Java Application in the AI Era"**, apresentada por Fernando Gomes no evento TDC São Paulo, aborda lições práticas e decisões de arquitetura na construção de produtos reais baseados em IA, focando em busca vetorial, RAG híbrido e mecanismos de segurança (_guardrails_).

---

### 1. Chamada ao LLM vs. Arquitetura Completa

Chamar o modelo de linguagem (LLM) representa a menor parte na construção do sistema. A arquitetura exige soluções integradas para:

- **Identidade e isolamento (Tenant):** Identificar quem está perguntando e garantir o isolamento estrito dos dados de cada cliente.
- **Recuperação (Retrieval) e Guardrails:** Buscar o contexto correto e impor regras do que nunca deve acontecer.
- **Custos, Observabilidade e Fallback:** Monitorar gastos com tokens e definir respostas determinísticas de contingência em caso de falhas.

---

### 2. Busca Híbrida (Hybrid RAG) e Chunking

A palestra destaca que a etapa de recuperação (_Retrieval_) do RAG não deve se limitar apenas à busca vetorial semântica:

- **Busca Vetorial vs. Lexical:** A busca por vetores entende o significado e sinônimos, mas falha em termos exatos, nomes próprios e códigos. A busca lexical (FTS/BM25) encontra termos exatos (ex: "Spring Boot 3.2"), mas ignora paráfrases.
- **Fusão via RRF (Reciprocal Rank Fusion):** O sistema executa ambas as buscas e combina suas classificações usando o algoritmo RRF (\\(score(d) = \sum 1 / (k + rank(r, d))\\) com \\(k=60\\)) para reordenar os resultados finais.
- **Chunking do tipo Parent-Child:** O texto é dividido em blocos menores (_child_) para vetorização e busca precisa. Quando um _child_ é selecionado, o texto pai (_parent_) é enviado ao LLM para preservar o contexto integral.

---

### 3. Banco de Dados: PostgreSQL + `pgvector`

Em vez de adotar bancos vetoriais dedicados (como Chroma ou Pinecone) ou clusters como Elasticsearch, a solução utiliza o **PostgreSQL com a extensão `pgvector`**:

- **Unificação:** Mantém os dados relacionais e vetoriais na mesma instância, eliminando latência de sincronização e complexidade de infraestrutura.
- **Isolamento de Tenant Nativo:** Filtra dados diretamente nas queries SQL (`WHERE tenant_id = :id`).
- **Desempenho:** Utiliza índices HNSW para busca vetorial aproximada (ANN) e busca textual completa nativa.

---

### 4. Guardrails e Proteção do Prompt

Para combater alucinações, vazamento de dados e _prompt injections_:

- **Configuração em JSON (`rag-instructions.json`):** Define de forma declarativa o papel do assistente, a restrição para usar apenas o contexto fornecido, regras de idioma e tópicos bloqueados (como política ou informações privadas).
- **Segurança no Código:** Aplica validações DTO antes do LLM, filtro de tenant automático via AOP, restrições rígidas no _system prompt_ para ignorar instruções maliciosas do usuário e parâmetros de geração controlados (`temperature = 0.3`, `maxTokens = 800`).
- **Graceful Fallback:** Em caso de erro na recuperação do contexto, o sistema não expõe falhas nem quebra o chat, retornando uma resposta padronizada.

---
