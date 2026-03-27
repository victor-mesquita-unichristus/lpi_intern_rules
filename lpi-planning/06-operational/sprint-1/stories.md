# Histórias da Sprint 1

## Contexto histórico

- A Sprint 1 é preservada como registro do escopo definido à época.
- Ela antecede a modelagem baseada em [`InternshipTerm`](lpi-planning/01-entities/internship-term.md).
- Portanto, as histórias abaixo não devem ser reinterpretadas como fonte de verdade do modelo atual.

## Observação posterior de escopo

- As histórias abaixo permanecem como registro histórico.
- Na implementação atual, `AgentIntegrator` não entra em escopo e `placementAgency` permanece como legado transitório.
- O fluxo de aditivo também não entra na sprint atual de implementação, embora a estrutura necessária para suportá-lo futuramente continue válida como direção de arquitetura.

## Histórias

### S1-US-01 — Criar estágio pelo fluxo de TCE

Como usuário administrativo, eu quero criar um estágio pelo fluxo de TCE para que o estágio seja formalmente registrado no sistema.

**Critérios de aceite**

- O fluxo cria um registro de estágio, e não uma entidade separada de TCE.
- O usuário deve informar aluno, empresa, supervisor, carga horária, remuneração e período.
- O supervisor selecionado deve pertencer à empresa selecionada.
- O aluno selecionado não pode receber um período de estágio sobreposto.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
- [`lpi-planning/03-cross-cutting/authorization.md`](lpi-planning/03-cross-cutting/authorization.md)

### S1-US-02 — Guiar o preenchimento do TCE com Step Modal

Como usuário administrativo, eu quero que o fluxo de TCE seja guiado em etapas para que o preenchimento fique mais claro e menos sujeito a erros.

**Critérios de aceite**

- O front-end usa Step Modal no fluxo de TCE.
- O usuário consegue navegar entre as etapas necessárias do processo de TCE.
- O feedback de validação aparece no ponto em que o usuário informa dados inválidos.
- A seleção opcional de agente integrador fica claramente separada dos dados contratuais obrigatórios.

**Dependências**

- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)

### S1-US-03 — Exibir indicativo de estágio ativo com consistência

Como usuário, eu quero ver se um estágio está ativo para entender rapidamente sua situação atual.

**Critérios de aceite**

- A UI exibe um indicativo claro de estágio ativo.
- O status exibido é consistente com o comportamento de negócio definido em [`internship.md`](lpi-planning/01-entities/internship.md).
- Estados inconsistentes de exibição são corrigidos.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)

### S1-US-04 — Corrigir inconsistências na exibição de dados do estágio

Como usuário, eu quero que as informações do estágio sejam exibidas com consistência para que eu possa confiar no que o sistema mostra.

**Critérios de aceite**

- Inconsistências existentes na exibição de dados do estágio são corrigidas.
- Dados opcionais vazios ou ausentes são exibidos com clareza.
- Dados históricos vinculados mantêm seu significado quando renderizados em telas de detalhe.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)
