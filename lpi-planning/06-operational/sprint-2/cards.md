# Cards da Sprint 2

## Cards

### S2-C01 — Implementar criação de termo de aditivo no backend

- Tipo: Back-end
- História: `S2-US-01`
- Escopo:
  - criar novo `InternshipTerm` com `type = ADDENDUM`
  - validar continuidade temporal
  - preservar histórico sem sobrescrita

### S2-C02 — Expor operação de aditivo por endpoint/caso de uso dedicado

- Tipo: Back-end
- História: `S2-US-01`
- Escopo:
  - criar operação dedicada de aditivo
  - mantê-la separada da edição genérica de estágio

### S2-C03 — Construir fluxo de UI para aditivo

- Tipo: Front-end
- História: `S2-US-01`
- Escopo:
  - renderizar campos do novo termo
  - exibir histórico prévio como referência
  - exibir feedback de validação de continuidade temporal

### S2-C04 — Implementar persistência de Agente Integrador e comportamento de soft delete

- Tipo: Back-end
- História: `S2-US-02`
- Escopo:
  - implementar regras de cadastro
  - preservar vínculo histórico com termos
  - ocultar registros inativos nos casos de uso padrão de seleção

### S2-C05 — Construir telas de gerenciamento de Agente Integrador

- Tipo: Front-end
- História: `S2-US-02`
- Escopo:
  - criar interações de lista e formulário
  - ocultar registros inativos no contexto padrão de listagem, quando aplicável
  - expor ação de exclusão de forma consistente com o comportamento de soft delete

### S2-C06 — Adicionar seleção opcional de Agente Integrador na UI do TCE

- Tipo: Front-end
- História: `S2-US-03`
- Escopo:
  - adicionar controle estruturado de seleção no termo inicial
  - impedir entrada por texto livre
  - excluir opções inativas

### S2-C07 — Adicionar suporte a Agente Integrador no contrato de TCE do backend

- Tipo: Back-end
- História: `S2-US-03`
- Escopo:
  - aceitar `agentIntegratorId` opcional em `InternshipTerm`
  - validar existência ativa antes da associação

## Cards pendentes relacionados à trilha posterior

### PEND-C01 — Consolidar persistência de soft delete em `Internship` e `InternshipTerm`

- Tipo: Back-end
- Depende de: [`soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)
- Status: `PENDENTE DE DECISÃO`

### PEND-C02 — Definir campos não contratuais editáveis em `Internship`

- Tipo: Produto + Back-end + Front-end
- Depende de: [`edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)
- Status: `PENDENTE DE DECISÃO`

### PEND-C03 — Definir fluxo operacional para edição contratual por snapshot fora do aditivo formal

- Tipo: Produto + Back-end + Front-end
- Depende de: [`edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)
- Status: `PENDENTE DE DECISÃO`
