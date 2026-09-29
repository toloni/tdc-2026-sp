A palestra **"Rodando agentes de IA no Kubernetes"**, apresentada por **Paulo Cerqueira (4Linux)**, aborda a necessidade de criar infraestruturas nativas e seguras no Kubernetes para suportar sistemas de Inteligência Artificial Agêntica através do projeto **Agent Sandbox**.

---

### 1. Contexto e a Evolução da IA

- **De LLMs a Agentes Autónomos:** Os modelos de linguagem (LLMs) evoluíram do reconhecimento e previsão de padrões de texto para a **IA Agêntica**, onde entidades autônomas tomam decisões, dividem tarefas em etapas e interagem diretamente com o ambiente externo (executando código, fazendo chamadas de rede e alterando sistemas de arquivos).
- **Sistemas Multi-Agentes:** A divisão de tarefas complexas entre múltiplos agentes especializados melhora a modularidade, a escalabilidade e a auditabilidade.
- **O Desafio da Segurança:** Como os agentes geram e executam código dinamicamente no ecossistema de produção, surgem sérios riscos de segurança e evasão de _guardrails_.

---

### 2. A Tese e o Conflito de Conceitos

A tese central da palestra é que **as primitivas tradicionais do Kubernetes são, por design, insuficientes e ineficientes para cargas de trabalho de agentes de IA**:

- **Agentes de IA** são processos de execução única (_singleton_), com estado persistente, que passam longos períodos ociosos e exigem mecanismos eficientes de pausa e retomada.
- **Containers Padrão do Kubernetes** compartilham o kernel do host, perdem sua identidade/sessão quando a pod é destruída e sofrem com a latência de _cold start_ ou desperdício de recursos.

---

### 3. O Projeto Agent Sandbox

Para resolver essa incompatibilidade, o grupo de trabalho do Kubernetes (**SIG Apps**) criou o projeto **Agent Sandbox**:

- **Objetivo:** Estender a API do Kubernetes para gerenciar e isolar ambientes de execução de agentes com forte segurança e controle de recursos.
- **Suporte a Runtimes Isolados:** Compatibilidade nativa com **gVisor** (mini-kernel no espaço do usuário), **Kata Containers** (micro-VMs) e **WASI/WebAssembly**.

---

### 4. Os 5 Componentes da Arquitetura

A solução é composta por novos Recursos Customizados (CRDs) e um serviço de rede dedicado:

1. **Sandbox (CRD):** Carga de trabalho _singleton_ e _stateful_. Permite alternar o estado entre `Running` e `Suspended` de forma declarativa pelo campo `spec.operatingMode`, mantendo o hostname, IP e armazenamento persistente ativos durante a pausa.
2. **SandboxTemplate (CRD):** O _blueprint_ reutilizável de configuração. Define limites rígidos de CPU/memória, imagens base, restrições de segurança e políticas de rede que não podem ser sobrescritas pelos consumidores.
3. **SandboxWarmPool (CRD):** Resolve o problema do _cold start_ mantendo um pool declarativo de instâncias pré-aquecidas, entregando o ambiente pronto em milissegundos.
4. **SandboxClaim (CRD):** Funciona de maneira análoga ao _PersistentVolumeClaim_ (PVC). Permite que aplicações solicitem a posse imediata de uma instância disponível no WarmPool.
5. **SandboxRouter (Plano de Dados):** Serviço instalado separadamente que intercepta o tráfego e roteia requisições dinamicamente para a Pod correspondente utilizando o cabeçalho `X-Sandbox-ID`.

---

### 5. Modelo de Responsabilidades e Uso Prático

- **Divisão de Papéis:** A Engenharia de Plataforma prepara o cluster e rountimes; a equipe de Infraestrutura/Operações define os templates e a capacidade dos WarmPools; e os Desenvolvedores focam na lógica dos agentes e no consumo via SandboxClaim.
- **Ferramental e SDKs:** O projeto oferece SDKs nativos em **Python** e **Go** para simplificar a integração.
- **Casos de Uso:**
  - Execução isolada de CLIs agênticas (como Claude Code ou GitHub Copilot CLI).
  - Instâncias locais de LLMs (como Ollama) rodando dentro do cluster.
  - Servidores MCP (_Model Context Protocol_) isolados por ferramenta.
  - Ambientes dedicados para frameworks multi-agentes como **LangGraph**, **CrewAI** ou **AutoGen**.

---

De forma direta, o **Agent Sandbox** serve para resolver um dilema prático: **como permitir que um agente de IA execute código, altere arquivos e acesse a rede com segurança, sem colocar a infraestrutura em risco e sem desperdiçar recursos**.

Um **agente de IA** difere de um aplicativo web tradicional porque ele toma decisões autônomas, lê e escreve no sistema de arquivos, realiza chamadas de rede e gera/executa código dinamicamente (código este que pode ser não confiável).

Se você tentar rodar esse agente em um container padrão do Kubernetes, surgem dois grandes gargalos:

- **Falta de isolamento de segurança:** Containers comuns compartilham o mesmo _kernel_ do sistema operacional do servidor host. Se o agente executar um código perigoso, malicioso ou sofrer um desvio de _guardrails_, ele pode comprometer o servidor ou outros serviços vizinhos.
- **Perda de sessão e _Cold Start_:** Agentes passam grande parte do tempo ociosos entre uma tarefa e outra, mas precisam preservar seu histórico, arquivos e contexto. Se o Kubernetes encerra o container para economizar recursos, a identidade e a sessão do agente morrem junto. Se decide criar um container novo do zero cada vez que o agente precisa agir, ocorre uma latência incômoda de inicialização (_cold start_).

---

### Como o Agent Sandbox resolve esses problemas?

O **Agent Sandbox** estende a API do Kubernetes para criar ambientes isolados e eficientes sob medida:

1. **Isolamento de Segurança Fortalecido:** Ele encapsula a execução do agente em runtimes isolados, como _gVisor_ (mini-kernel isolado) ou _Kata Containers_ (micro-VMs). Isso garante que, mesmo que o agente rode um código inseguro, a execução fique restrita à caixa de areia sem expor o sistema operacional do host.
2. **Pausa e Retomada sem Perda de Dados:** Permite alternar o estado do ambiente para suspenso (`Suspended`) quando o agente está ocioso. Isso libera recursos computacionais sem perder o endereço IP, o nome de host ou o armazenamento de arquivos persistente do agente.
3. **Ambientes Prontos em Milissegundos:** Através do _SandboxWarmPool_, o cluster mantém uma reserva de ambientes pré-inicializados e "aquecidos". Quando uma nova requisição chega, o ambiente é entregue de forma quase instantânea, eliminando o problema do _cold start_.
4. **Identidade Estável e Dedicada:** Cada agente recebe um espaço de trabalho único e persistente (_singleton_ e _stateful_), ideal para manter o estado da aplicação.

Em resumo, o Agent Sandbox serve para fornecer ao agente de IA um **playground seguro, de inicialização instantânea e com estado persistente** dentro do Kubernetes.
