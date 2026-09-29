A palestra **"From BFF to Server-Driven UI: A Spec-Driven Approach"**, apresentada por Danilo Pereira De Luca no _The Developer's Conference_ (TDC), aborda a evolução das arquiteturas de front-end e back-end em ecossistemas de microsserviços.

---

### 1. **Evolução Arquitetural: Do Frontend Direto ao Server-Driven UI (SDUI)**

- **Sem BFF (Backend for Frontend):** As aplicações client (Android, iOS, Web) comunicam-se diretamente com múltiplos serviços de back-end. Isso gera chamadas excessivas de rede, acoplamento entre front-end e back-end, lógica de agregação no cliente e inconsistência de regras de negócio entre plataformas.
- **Com BFF:** A camada de BFF centraliza e agrega as chamadas em uma única interface. No entanto, utilizar o BFF apenas como agregador de dados ainda gera problemas como acoplamento, inconsistência de experiência e um "spaghetti de contextos".
- **Transição para SDUI:** O BFF evolui de um mero agregador de APIs/dados para um **compositor de experiências**. Em vez de o cliente decidir sozinho o layout, o back-end e o front-end passam a **compartilhar uma linguagem comum** que descreve a interface via JSON.

---

### 2. **Garantindo Consistência com Spec-Driven Development (SDD)**

- **O Desafio do SDUI:** O BFF envia a descrição dos componentes, mas as plataformas (Android, iOS e Web) precisam interpretá-los de forma idêntica.
- **Spec-Driven Development:** Adota-se a especificação como a **fonte única da verdade** (_source of truth_) para a comunicação entre sistemas. Na era da IA, essas especificações passam a orientar o que e como agentes de automação devem construir. No SDD, **o código torna-se o detalhe de implementação da especificação**, declarando a intenção do sistema.

---

### 3. **Divisão Clara de Responsabilidades**

A palestra destaca o papel de cada camada no modelo SDUI com SDD:

- **BFF (Decide o _que_ e o _como_):** Define o conteúdo (dados), o comportamento (ações e interações), a ordem/composição na tela e a família de estilo pré-definida dos componentes (ex.: `card-venue`, `button-primary`).
- **App / Design System (Define _como aparece_):** Gerencia a aparência visual — dimensões, formato de bordas, paleta de cores (incluindo modo escuro), tipografia, espaçamentos, animações e estados dos componentes (`loading`, `disabled`, `error`).

---

### 4. **Organização das Especificações e Repositório Central**

- **Specs Compartilhadas (Core):** Definem componentes, propriedades, eventos, regras de negócio e comportamentos aplicáveis a todas as plataformas.
- **Extensões por Plataforma:** Specs específicas para capabilities e componentes nativos de Android, iOS e Web.
- **Execução:** O BFF utiliza as specs compartilhadas para montar os JSONs de tela, enquanto cada app lê essas especificações e renderiza a interface utilizando seu respetivo Design System.

---

### 5. **Desafios e Visão de Futuro**

- **Processo de Trabalho:** Exige trazer a escrita de especificações para perto dos times de Produto e utilizar agentes automatizados para sincronização e revisão de specs.
- **Evolução e Custos de Contexto:** Com o crescimento dos times e o acúmulo de especificações, a utilização de ferramentas de IA baseadas em specs gera contextos maiores, resultando no consumo de mais tokens e aumento nos custos operacionais.

---
