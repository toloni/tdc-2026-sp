A palestra **"APIs como Infraestrutura: quando integração vira arquitetura"**, apresentada por **André Rácz** e **Yan Borowski** no **TDC São Paulo 2026** (Trilha APIs & Microservices), aborda o impacto de tratar integrações e APIs como decisões meramente técnicas, demonstrando como falhas de integração afetam diretamente a arquitetura e a operação das empresas.

---

### **1. A Tese Central: Stack vs. Integração**

- **Decisão local vs. impacto distribuído:** Alterar a _stack_ ou o banco de dados de um serviço é uma decisão local e reversível. Já publicar um _endpoint_ gera uma decisão de integração **irreversível e distribuída**, pois o custo da mudança é transferido para o consumidor.
- **Impacto no negócio:** Escolhas de _stack_ raramente paralisam a operação da empresa, enquanto falhas de integração podem paralisar a logística e a entrega de produtos.

---

### **2. Os Três Atos do Problema**

A palestra organiza a evolução dos problemas de integração em três níveis sobrepostos:

#### **Ato 1: O Nível Técnico (_"Foi um bug"_)**

- **Sintomas:** Múltiplas versões e realidades do mesmo contrato rodando em paralelo em diferentes regiões, além de consumidores legados não mapeados que ficam de fora de avisos de mudança.
- **A armadilha da burocracia:** Conhecer conceitos como resiliência, idempotência, versionamento e _retry_ não é o maior obstáculo ("nada disso é difícil"). O problema é ter pipelines repletos de testes e filas de aprovadores, mas **zero mecanismos** para identificar quem realmente depende do contrato. Isso gera **máxima burocracia e mínima proteção**.

#### **Ato 2: O Nível Arquitetural (_"Não era um bug"_)**

Surge quando a organização atinge marcas de **1.000+ endpoints publicados** sem catálogo, sem _ownership_ e sem mapa de consumo. Esse cenário revela **Três Descompassos Arquiteturais**:

1. **Consumidores Invisíveis:** O crescimento de \\(n\\) serviços gera \\(n^2\\) caminhos possíveis, tornando impossível prever os fluxos de consumo.
2. **Ciclo de Vida:** Microsserviços realizam múltiplos _deploys_ diários, enquanto sistemas legados/ERPs mudam de 2 a 3 vezes por ano. Aplicar o mesmo processo de mudança para ambos bloqueia quem precisa mudar diariamente e não protege adequadamente o sistema estável.
3. **Capacidade:** Camadas de nuvem elásticas escalam sem limite e despejam volume sobre sistemas legados de capacidade fixa. Como o contrato descreve o formato da API, mas raramente sua capacidade, o sistema acaba ruindo por saturação de recursos.

- **Solução arquitetural:** _Rate Limit_ padrão (HTTP 429) protege o provedor punindo o consumidor. A abordagem correta é nivelar a carga e controlar a vazão, comprando disponibilidade ao preço de aceitar maior latência nos fluxos tolerantes a atraso. **Integração é o regulador onde as diferenças entre sistemas são negociadas**.

#### **Ato 3: O Nível Organizacional (_"Nunca foi um bug"_)**

- **A Lei de Conway na prática:** Desenhar um _endpoint_ define quem pode bloquear o trabalho de quem dentro da organização.
- **Visão fragmentada:** Na ausência de contratos de consumo transparentes, ninguém enxerga o fluxo ponta a ponta. Quando ocorre uma falha, a primeira reunião é para descobrir de quem é o problema.
- **O Custo em Cascata:** Uma quebra de contrato desencadeia atrasos de _lead time_, acúmulo de caminhões, atraso de entregas e impacto no faturamento.

---

### **3. Diagnóstico de Risco**

A palestra propõe uma matriz de diagnóstico. Se ao menos três dos pontos abaixo forem verdadeiros na sua organização, **a integração já é o seu maior risco arquitetural**:

- **Técnica:** É possível quebrar um consumidor sem o pipeline reclamar; existem múltiplas formas de autenticação interna; o comportamento da API muda sem alterar o número da versão.
- **Arquitetural:** Ninguém responde em 30 segundos quem é o dono de um _endpoint_; não é possível listar consumidores sem abrir chamado; o fluxo mais lento e seu limite de capacidade são desconhecidos.
- **Organizacional:** A data de _release_ depende de um time ausente no _planning_; há janelas do mês onde nada pode ser implantado sem motivo claro; reuniões pós-incidente buscam culpados em vez de causas.

---

### **4. Plano de Ação para a Segunda-Feira**

Para mitigar os descompassos, os palestrantes recomendam quatro ações imediatas:

1. **Registro antes de ferramenta:** Comece o mapeamento com uma planilha simples de _ownership_ e consumo, sem esperar pela implementação de um catálogo formal.
2. **Contrato verificado em pipeline:** Substitua aprovações manuais por verificações automatizadas de contrato na esteira de CI/CD.
3. **Capacidade dentro do contrato:** Garanta que a vazão suportada pelo destino e o tratamento do excedente estejam definidos explicitamente no acordo.
4. **Ownership por time e liderança:** Atribua a responsabilidade do domínio a um time com liderança clara, evitando indicar indivíduos isolados ou equipes genéricas sem dono.

---

### **Conclusão**

> _"Stack é decisão. Integração é acordo. Por isso integração é arquitetura. E arquitetura é responsabilidade de liderança."_
> _"Engenharia previne o incidente. Só liderança previne a classe do incidente."_
