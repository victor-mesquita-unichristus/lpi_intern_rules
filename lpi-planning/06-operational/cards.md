# Cards Operacionais

Este arquivo decompõe as histórias atuais das sprints em cards executáveis para um time com 2 estagiários de front-end e 2 estagiários de back-end.

## Cards da Sprint 1

### S1-C01 — Consolidar regras de validação do TCE no backend

- Tipo: Back-end
- História: `S1-US-01`
- Escopo:
  - aplicar validações de criação de estágio
  - aplicar consistência de relacionamentos
  - aplicar proteção contra sobreposição
  - retornar erros de validação utilizáveis

### S1-C02 — Refinar contrato do endpoint de criação de TCE

- Tipo: Back-end
- História: `S1-US-01`
- Escopo:
  - alinhar payload com os campos obrigatórios do TCE
  - tratar `agentIntegratorId` opcional
  - alinhar dados de resposta consumidos pela UI

### S1-C03 — Implementar estrutura do Step Modal de TCE

- Tipo: Front-end
- História: `S1-US-02`
- Escopo:
  - definir etapas
  - manter estado de navegação
  - validar progressão entre etapas

### S1-C04 — Integrar Step Modal de TCE com o fluxo de criação no backend

- Tipo: Front-end
- História: `S1-US-01`, `S1-US-02`
- Escopo:
  - enviar payload final
  - exibir feedback de validação de campo e de fluxo
  - tratar estados de sucesso e erro

### S1-C05 — Exibir indicador de estágio ativo na UI

- Tipo: Front-end
- História: `S1-US-03`
- Escopo:
  - padronizar indicação de estágio ativo
  - usar dados de status consistentes com o backend

### S1-C06 — Corrigir inconsistências de renderização em detalhe/lista de estágio

- Tipo: Front-end
- História: `S1-US-04`
- Escopo:
  - normalizar renderização de campos opcionais
  - corrigir apresentação inconsistente de estados vazios

## Cards da Sprint 2

### S2-C01 — Implementar regras de aditivo no backend

- Tipo: Back-end
- História: `S2-US-01`
- Escopo:
  - alterar apenas datas de aditivo
  - validar comportamento permitido de aditivo
  - persistir resultado consistente com o status

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
  - renderizar apenas campos de aditivo
  - bloquear campos que não pertencem ao aditivo
  - exibir feedback de validação de datas

### S2-C04 — Implementar persistência de Agente Integrador e comportamento de soft delete

- Tipo: Back-end
- História: `S2-US-02`
- Escopo:
  - implementar regras de cadastro
  - preservar vínculo histórico
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
  - adicionar controle estruturado de seleção
  - impedir entrada por texto livre
  - excluir opções inativas

### S2-C07 — Adicionar suporte a Agente Integrador no contrato de TCE do backend

- Tipo: Back-end
- História: `S2-US-03`
- Escopo:
  - aceitar `agentIntegratorId` opcional
  - validar existência ativa antes da associação

## Cards pendentes que dependem de decisões ainda não resolvidas

### PEND-C01 — Consolidar persistência de soft delete em estágio

- Tipo: Back-end
- Depende de: [`soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)
- Status: `PENDENTE DE DECISÃO`

### PEND-C02 — Definir campos editáveis para manutenção de estágio antes do início

- Tipo: Produto + Back-end + Front-end
- Depende de: [`edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)
- Status: `PENDENTE DE DECISÃO`
