Esta palestra, intitulada **"Harness Engineering: o próximo passo"** e apresentada por **Michael Douglas Barbosa Araújo** no **TDC São Paulo 2026**, aborda a transição do foco em modelos isolados de IA para a construção de sistemas de execução confiáveis.

---

### 1. O Problema da Fragilidade dos Sistemas de IA

- **Capacidade vs. Confiabilidade:** Embora os modelos de linguagem tenham evoluído e forneçam respostas melhores, os sistemas continuam frágeis. Ferramentas executam sem reconciliar _timeouts_ ou retries, e códigos compilados acabam indo para produção sem as devidas checagens e políticas.
- **A Limitação do Prompt:** O diferencial na engenharia de IA deixou de ser o prompt isolado. Sem o **harness** (o ambiente de execução, validação, memória e governança que envolve o modelo), ferramentas passam a ser apenas APIs expostas a uma intenção probabilística.
- **Redução de Variância:** Modelos mais fortes aumentam a capacidade e o espaço do possível; o harness reduz a variância operacional e delimita o espaço do que pode dar errado.

---

### 2. O que é Harness Engineering?

O **Harness Engineering** consiste em desenhar uma "máquina de confiabilidade" ao redor da IA. O fluxo de execução do harness engloba: **Prompt \\(\rightarrow\\) Context \\(\rightarrow\\) Tools \\(\rightarrow\\) State \\(\rightarrow\\) Gates \\(\rightarrow\\) Recovery**. Suas responsabilidades dividem-se em três pilares:

1. **Contexto:** Gerencia como o sistema monta, limita, versiona e explica as informações apresentadas ao modelo.
2. **Execução:** Controla como as ações são planejadas, autorizadas, executadas ou revertidas.
3. **Evidência:** Valida, rastreia e vincula cada resultado ao artefato final entregue.

---

### 3. Componentes Fundamentais do Harness

- **Estruturação da Demanda (_Intake_):** Antes de o modelo raciocinar, o harness classifica a intenção (ex.: _bugfix_, _feature_, análise), resolve ambiguidades e define o nível de risco (leitura, escrita, produção, impacto financeiro).
- **Engenharia de Contexto e Contrato:** Define limites de volume, procedência e validade das informações que chegam ao modelo, evitando falta de escopo (ruído), falta de rastreabilidade e estouro de custos (_budget_).
- **Memória como Estado Operacional:** A memória do sistema não é um simples histórico de conversa, mas sim a gestão da **intenção**, do **plano aprovado**, dos **efeitos externos executados** e das **evidências** obtidas.
- **Validação Determinística (_Gates_):** A saída da IA não é aceita como verdade absoluta. O harness aciona verificadores determinísticos, lints, checagens de tipo, testes automatizados e políticas de segurança antes de autorizar a entrega.
- **Controle de Loop e Autonomia:** Para conter riscos, o harness estabelece limites de passos e recursos (_step budget_), condições de saída (_stop conditions_) e critérios claros para interromper a autonomia do agente.
- **Recuperação de Falhas (_Recovery_):** O tratamento de exceções é central: o sistema realiza _checkpoints_ e sabe restaurar e reconciliar a execução sem repetir efeitos colaterais perigosos.

---

### 4. Governança e Aplicação no Desenvolvimento (AI-DLC)

- **Intervenção Humana (_Human-in-the-Loop_):** Humanos não precisam aprovar todas as etapas, mas sim intervir nos pontos de alto risco — como ações com efeito externo irreversível (PRs, deploys, cobranças), alta ambiguidade ou custos elevados.
- **Arquitetura Reutilizável:** O harness separa a orquestração da aplicação e centraliza regras, contexto, _skills_ e políticas em uma camada central (como em um _Backend for Agents_).
- **Especificações e Subagentes:** Intenções são convertidas em contratos testáveis (SPECs). A execução pode ser delegada a **subagentes especializados** (ex.: frontend, backend, QA), que operam com contextos restritos sob o mesmo contrato.
- **Ferramental Integrado:** Utiliza arquivos como `AGENTS.md` para estabelecer regras e fluxos, ferramentas como _Graphify_ para mapear dependências do repositório, _Skills_ para reutilizar conhecimento procedural e _MCP_ (_Model Context Protocol_) para expor capacidades externas de forma segura.
- **Versionamento Conjunto:** Alterar o modelo de IA sem versionar o harness invalida qualquer comparação, pois os critérios do sistema também mudam.

---

### Conclusão

O futuro da IA não está apenas em selecionar o modelo com maior capacidade, mas em **construir o melhor sistema para que ele opere de forma confiável, governável e repetível**.
