# Cards da Sprint 1

## Contexto histórico

- Os cards desta sprint preservam o recorte operacional original.
- Eles antecedem a introdução de [`InternshipTerm`](lpi-planning/01-entities/internship-term.md) como entidade do domínio.

## Observação posterior de escopo

- Estes cards não devem ser reinterpretados retroativamente como escopo obrigatório da implementação atual.
- Na implementação atual, `AgentIntegrator` está fora de escopo e `placementAgency` permanece como legado transitório.
- O fluxo de aditivo também não integra a sprint atual de implementação; apenas a preparação estrutural correspondente permanece relevante.

## Cards

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
