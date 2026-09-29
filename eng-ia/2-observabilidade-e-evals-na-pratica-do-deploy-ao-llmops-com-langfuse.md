A palestra **"Observabilidade e Evals na prática: do deploy ao LLMOps com Langfuse"**, apresentada por **Kelvin Pacheco Pacheco** (Engenheiro de Machine Learning na Factored.ai), aborda como estruturar o ciclo de vida e o monitoramento de aplicações baseadas em modelos de linguagem (LLMs) utilizando a plataforma **Langfuse**.

---

### 1. O Problema do Monitoramento Tradicional

- **Limitação das métricas convencionais**: Ferramentas clássicas de APM monitoram disponibilidade, latência e código HTTP (ex.: 200 OK), mas não conseguem medir a qualidade das respostas de uma LLM.
- **"Tudo verde, menos a qualidade"**: Um prompt alterado pode gerar queda nas conversões da empresa e aumento de reclamações sem causar _crashes_ na aplicação, sem alterar os custos e mantendo os logs tradicionais com status "normal".

---

### 2. Tracing: A Caixa-Preta do Voo

O **trace** funciona como o registro completo de telemetria que explica como o modelo tomou cada decisão. Ele é dividido em três dimensões principais:

- **Contexto**: Entrada do usuário, histórico da conversa, versão do prompt e dados da sessão.
- **Decisão**: Modelo e parâmetros utilizados, contagem de tokens, custo financeiro, latência e raciocínio intermediário.
- **Ação**: Chamadas de ferramentas (_tool calls_), parâmetros enviados, retorno/erros e a resposta final entregue.

A palestra demonstra esse conceito na prática com o agente **ClimaCasa** (uma empresa fictícia de manutenção de ar-condicionado), construído com **PydanticAI**, integrado a APIs externas (Google Maps e Cal.com) e transmitindo telemetria em tempo real para o painel do Langfuse.

---

### 3. Gestão e Versionamento de Prompts

- **Prompt como configuração em produção**: Prompts não devem ser tratados como simples textos hardcoded no código, mas sim como configurações gerenciadas em ambiente de produção.
- **Ciclo de vida do prompt**:
  - **Versionar**: Prompts imutáveis com acompanhamento de modelo, parâmetros e histórico auditável.
  - **Validar**: Testes com datasets fixos, métricas de avaliação (_evals_) comparáveis e revisão humana.
  - **Promover**: Uso de rótulos (ex.: `production`), testes A/B ou implantações em canário.
- **Rollback sem redeploy**: Ao desacoplar o prompt, os parâmetros e as ferramentas do ciclo de lançamento do software, é possível reverter a versão do prompt em 1 segundo sem necessidade de acionar um pipeline de CI/CD.

---

### 4. Avaliações (Evals) e Hierarquia de Verificação

As **evals** transformam traces brutos em indicadores concretos de qualidade. A palestra enfatiza que não se deve usar um "LLM como juiz" (_LLM-as-a-judge_) para todas as situações, propondo uma **hierarquia de verificação**:

1. **Verificações Determinísticas (Código)**: Checagens rápidas de alta frequência, como validação de JSON, esquemas via regex e presença obrigatória de argumentos de ferramentas.
2. **LLM como Juiz (_LLM-as-a-Judge_)**: Avaliação de critérios semânticos, tais como relevância, fidelidade às fontes (_grounding_), tom da resposta e completude.
3. **Revisão Humana**: Análise direta para casos ambíguos, calibração dos avaliadores automáticos e inspeção de incidentes críticos.

**Exemplo Prático (Presença ≠ Intenção)**: Uma busca por palavras-chave (_fuzzy match_) pode identificar o nome de uma cidade na mensagem do usuário e gerar um falso positivo (score 1.0). No entanto, um avaliador de intenção semântica detecta quando a cidade do pedido realmente continua ambígua (ex.: _"Minha mãe mora em Santos. Vocês atendem na minha cidade?"_), atribuindo nota 0.0 para evitar respostas incorretas do agente.

---

### 5. O Ciclo de LLMOps

A palestra resume o **LLMOps** como um ciclo contínuo composto por quatro etapas interligadas:

1. **Tracing**: Observar decisões, execução e custos em produção.
2. **Analyzing**: Detectar anomalias, falhas e gargalos de latência.
3. **Prompting**: Versionar e iterar prompts utilizando rótulos de ambiente.
4. **Evaluating**: Validar a qualidade continuamente e evitar regressões.
