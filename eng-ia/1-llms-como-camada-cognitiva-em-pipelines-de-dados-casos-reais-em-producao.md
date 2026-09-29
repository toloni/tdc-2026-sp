A palestra **"LLMs como camada cognitiva em pipelines de dados: casos reais em produção"** foi ministrada por **Juliana Maria Lopes**, Gerente de AI & Data na GFT Technologies. O tema central aborda como integrar modelos de linguagem em arquiteturas de dados de forma confiável e com governança de engenharia de software.

---

### 1. O que um LLM faz de verdade (e suas limitações)

- **Funcionamento probabilístico**: Um LLM faz apenas uma coisa: prevê qual é o próximo pedaço de texto. Ele **não** consulta bancos por conta própria, **não** realiza cálculos matemáticos (prevê o texto de um número) e **não** sabe o que não sabe.
- **Engenharia de tokens e contexto**: O modelo lê tokens, e o tamanho da entrada é uma decisão crítica de engenharia. Tabelas gigantescas exigem fatiamento, o que altera resultados porque o modelo perde o que fica de fora.
- **A anatomia mínima do prompt**: Para funcionar como um programa, o prompt deve conter 5 elementos: **Papel**, **Lista fechada de opções**, **Exemplos (few-shot)**, **Formato de saída (schema exigido)** e **Escape** (uma opção válida para incerteza, como `<None>`).
- **Variabilidade e alucinação**: Mesmo com temperatura zero, a determinicidade total não é garantida. A alucinação é tratada não como defeito de fábrica, mas como consequência direta de o modelo sempre buscar uma continuação provável. Para reduzi-la, exigem-se saídas estruturadas em **JSON** validadas antes da gravação.

---

### 2. Formas de ligar o modelo aos dados

A palestra detalha três formas de fornecer contexto ao LLM:

- **Prompt**: Injeta o dado diretamente na instrução (indicado para dados pequenos que cabem na janela de contexto).
- **RAG (Retrieval-Augmented Generation)**: Busca o trecho relevante via _embedding_ e injeta na chamada (indicado para bases grandes e dinâmicas).
- **Fine-Tuning**: Ajusta os pesos com exemplos próprios quando o formato ou estilo precisa ser fixo.
- **Regra de arquitetura**: **"RAG resolve conhecimento, fine-tuning resolve comportamento"**.

---

### 3. A Camada Cognitiva e Onde NÃO Usar LLMs

- **A Regra de Ouro**: A etapa cognitiva introduz probabilística no pipeline analítico para operar sobre _significado_. Por isso, ela **nunca é a última etapa** — sua saída é uma proposta que exige verificação determinística ou aprovação humana.
- **Onde NÃO usar**: Em validações de regras determinísticas, checagens de formatação, tarefas onde o erro é irreversível sem revisão humana, cenários de volume enorme com ganho marginal e situações que exigem cálculos exatos. Usar LLM onde uma regra resolveria é considerado o erro de arquitetura mais caro.

---

### 4. Engenharia de Prompts e Governança em Produção

- **Prompt como Artefato Versionado**: O prompt é salvo em arquivo e submetido a revisão de código e testes.
- **Injeção de Contexto Estruturado**: Além da pergunta, a chamada recebe dicionários de schema, códigos do domínio, catálogos de antipadrões e exemplos anonimizados.
- **Verificador Determinístico**: A resposta do modelo é checada por regras fixas que aplicam proibições absolutas e convenções do projeto antes de qualquer publicação.
- **Níveis de Alçada**:
  - **Executa sozinho**: leitura, classificação, explicação e reconciliação de números.
  - **Propõe e espera**: alterações em código ou modelos.
  - **Nunca decide**: aceite funcional, certificação do modelo semântico e desligamento de sistemas legados.
- **Testes de Regressão (Gabarito)**: Cada prompt possui entre 7 a 12 casos de teste com entrada e saída esperadas. Novos defeitos encontrados em campo convertem-se em novos casos de teste.

---

### 5. Estudo de Caso Real e Impacto

- **Cenário**: Migração do parque de BI (MicroStrategy para Microsoft Fabric e Power BI) de uma grande operadora de saúde, envolvendo **12.887 objetos** com regras ocultas em SQL sem documentação.
- **Execução**: Dividida em 4 tarefas principais (Classificar, Enriquecer, Detectar e Documentar) ao longo de 6 etapas e 17 artefatos/skills encadeados.
- **Resultados**: **83% de redução no tempo de desenvolvimento por relatório**. Tarefas como traduzir a definição de origem caíram de 2–3 dias para 30 minutos mais revisão.
- **Limitações**: A camada reduziu semanas de trabalho para horas, mas não corrigiu problemas de premissas de ambiente incorretas (como bases de homologação desatualizadas).

A grande lição da palestra é que usar LLM para calcular números ou aplicar regras fixas é o erro de arquitetura mais caro. O valor real está em usar o modelo como essa **camada de interpretação e tradução** em tarefas complexas de engenharia, mantendo o controle com verificadores determinísticos e salvando a cadeia de _skills_ para ser reutilizada em projetos futuros
