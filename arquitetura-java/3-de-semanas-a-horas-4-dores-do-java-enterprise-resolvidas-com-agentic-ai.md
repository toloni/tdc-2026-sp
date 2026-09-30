A palestra **"De semanas a horas: 4 dores do Java Enterprise resolvidas com Agentic AI"**, apresentada por **Elder Moraes**, aborda como o uso de agentes de Inteligência Artificial pode acelerar e destravar a manutenção e evolução de sistemas legados em Java Enterprise.

A apresentação parte da realidade de muitos desenvolvedores que assumem projetos antigos — por exemplo, um repositório com quase 20 mil linhas de código, centenas de arquivos e _imports_ `javax`, sem testes e sem pipeline de integração contínua, em um cenário onde o **Java 8 ainda está presente em produção** em uma parcela significativa do mercado.

---

### **As 4 Dores Principais e Suas Soluções com Agentic AI**

1. **1ª Dor: Entender (Onboarding e Codebases sem Dono)**
   - **O problema:** Em arquiteturas legadas, pequenas dúvidas de negócio (como _"onde eu mexo para alterar a taxa de uma ordem?"_) tornam-se complexas devido a múltiplas implementações de interfaces e ausência de testes.
   - **Solução com IA:** Usando agentes de IA no terminal, é possível mapear todo o fluxo de uma requisição e identificar os pontos exatos de alteração em questão de segundos (ex.: 47 segundos). Isso reduz consideravelmente o tempo de _onboarding_ e acelera a produtividade até os primeiros _pull requests_.

2. **2ª Dor: Testar (Código Legado Sem Testes)**
   - **O problema:** Projetos sem a estrutura `src/test`, com regras de negócio duplicadas e validação feita manualmente em tela.
   - **Solução com IA:** Aplicação de **testes de caracterização** (conceituados por Michael Feathers) para documentar o comportamento real e atual do sistema. Por meio de uma sequência de prompts direcionados (ajuste de POM, criação de testes unitários puros e simulação de dependências com mocks), a IA gera uma suíte verde com cobertura de testes do zero, garantindo a segurança necessária para refatorações.

3. **3ª Dor: Migrar (Atualizações de Versão, ex.: Java 8 para Java 27)**
   - **O problema:** A migração não é apenas trocar a versão no POM; envolve lidar com a mudança do namespace `javax` para `jakarta` e com a remoção ou encapsulamento de APIs críticas ao longo das versões do OpenJDK (como remoção do `javax.xml.bind`, desativação do _Security Manager_ e alteração no `sun.misc.Unsafe`).
   - **Solução com IA + Automação Determinística:** Combinação de ferramentas determinísticas (como o _OpenRewrite_) para a base da migração com o trabalho do agente de IA para solucionar as lacunas restantes até o JDK 27. Essa abordagem reduz substancialmente o tempo total de migração e a taxa de erros.

4. **4ª Dor: Automatizar (Pipelines de CI/CD do Zero)**
   - **O problema:** Necessidade de automatizar processos de verificação e build contínuo seguindo o princípio de automatizar aquilo que se consegue explicar.
   - **Solução com IA:** Construção automatizada de _workflows_ de GitHub Actions via prompts. O agente cria o pipeline, configura _gates_ de cobertura de código (ex.: JaCoCo) e analisa os logs de falha para aplicar correções automaticamente.

---

### **O Papel do Desenvolvedor no Novo SDLC**

- **Ganhos de produtividade:** Tarefas de mapear alterações, criar suítes de teste, atualizar dependências/APIs e criar CI/CD passam de semanas ou dias para **horas ou minutos**.
- **O ciclo de vida de desenvolvimento (SDLC) não muda:** O agente passa a realizar o trabalho pesado de **leitura massiva, escrita, repetição e exploração**.
- **Decisão e Responsabilidade:** O desenvolvedor continua sendo a figura central que decide **o que é correto, o que é aceitável e o que vai para produção**. O código final em produção é de total responsabilidade do desenvolvedor, mesmo que a IA tenha assinado o _commit_.

---
