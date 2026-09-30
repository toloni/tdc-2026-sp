A palestra **"O dev Java depois da IA: Fundamentos, arquitetura e decisões que ainda dependem de você"**, apresentada no TDC São Paulo 2026 pelos palestrantes Luis Fabrício De Llamas e Luiz Gustavo dos Santos Real, aborda o impacto real da inteligência artificial no desenvolvimento de software e no ecossistema Java.

---

### 1. O Cenário Atual do Java e a Adoção de IA

- **Relevância Mantida**: **62% das empresas já utilizam Java para construir funcionalidades de IA** (um crescimento em relação aos 50% em 2025), e **31%** relatam que mais da metade de suas aplicações Java já contam com IA embutida.
- **Adoção Massiva**: **84% dos desenvolvedores usam ou planejam usar ferramentas de IA para programar**. A Gartner projeta que a adoção corporativa entre engenheiros chegará a 75% até 2028.

---

### 2. A Ilusão de Velocidade e a Confiança em Queda

- **Queda na Confiança**: Apesar do aumento no uso, a **confiança no código gerado caiu de 40% (2024) para 29% (2025)**.
- **O Padrão que Engana**: O erro mais perigoso é aquele que parece correto na primeira leitura, passa na revisão e só falha semanas depois em produção. Além disso, **45% dos devs afirmam que depurar código gerado por IA leva mais tempo do que escrever do zero**.
- **Produtividade Real vs. Percebida**:
  - Os desenvolvedores esperavam um ganho de **+24%** em produtividade antes de usar IA.
  - Medições reais com devs experientes mostraram um resultado negativo de **-19% de tempo adicional gasto**.
  - Mesmo assim, **+20% acreditavam ter ficado mais rápidos**, demonstrando uma forte ilusão de velocidade.
- **Mudar Processos vs. Apenas Dar Ferramentas**: Dar apenas a ferramenta não altera significativamente os resultados da maioria das empresas. Ganhos expressivos (como **10x mais rápido pela metade do custo**) só ocorrem em organizações que redesenham todo o seu fluxo de trabalho em torno da IA.

---

### 3. O Gargalo de Segurança no Código Gerado

- **Impacto Geral**: **93% das organizações já sofreram ao menos uma violação de segurança** decorrente de aplicações vulneráveis.
- **Falhas em Modelos de IA**: **45% do código gerado por IA falha em testes de segurança** em mais de 150 modelos avaliados.
- **Java sob o Microscópio**: O código Java gerado por IA apresentou **71% de taxa de falha em testes de segurança**, o pior desempenho entre as quatro linguagens avaliadas (Python, C#, JavaScript e Java).
- **Risco Consciente**: **70% dos devs reconhecem que código gerado por IA contém mais vulnerabilidades**, porém **30% enviam código vulnerável para produção mesmo sabendo do risco**.
- **Iterar sem Julgamento Piora o Cenário**: Pedir para a IA refazer o código repetidamente sem revisão crítica aumenta em **+37% as vulnerabilidades críticas** após 5 iterações.

---

### 4. Os Fundamentos e a Liderança Técnica

- **O que a IA Não Decide por Você**:
  1. Arquitetura e limites do sistema
  2. Modelagem de concorrência
  3. Trade-offs de performance
  4. O que testar e os motivos dos testes
- **A Competência nº 1 do Dev Sênior**: A **leitura crítica de código** deixou de ser opcional e se tornou a habilidade central do desenvolvedor.
- **Três Pilares da Liderança Técnica**:
  - **Julgamento**: Saber quando a sugestão da IA está correta e quando não está.
  - **Contexto**: Entender o sistema de forma holística, além da função exibida na tela.
  - **Responsabilidade**: Assinar em baixo e responder por aquilo que vai para produção.

---

### 5. Quatro Hábitos Práticos Recomendados

1. **Revisar segurança antes de aceitar**, e não após a ocorrência de um incidente.
2. **Não fazer merge** do que você não conseguiria explicar detalhadamente em uma reunião.
3. **Testar antes de confiar**, mesmo quando o código "parece" certo à primeira vista.
4. **Assumir a responsabilidade total** pelo código gerado por IA que você aprovou.

---

### Mensagem Final

> **"A IA acelera a digitação. Não substitui a engenharia."**
