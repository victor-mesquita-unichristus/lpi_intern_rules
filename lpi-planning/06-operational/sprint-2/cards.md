# Cards da Sprint 2

## Blocos de execução

### S2-C01 — Criar persistência de `InternshipTerm` e migrations

- Tipo: Back-end
- História: `S2-US-01`
- Escopo:
  - criar a estrutura persistida de [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
  - definir migrations da nova modelagem
  - remover dependência operacional dos campos contratuais antigos em [`Internship`](lpi-planning/01-entities/internship.md)

### S2-C02 — Refatorar domínio de estágio e leitura do termo vigente

- Tipo: Back-end
- História: `S2-US-02`
- Escopo:
  - adaptar domínio e services de estágio
  - mover supervisor para o termo
  - consolidar leitura do termo vigente

### S2-C03 — Refatorar casos de uso e contratos de TCE e aditivo no backend

- Tipo: Back-end
- História: `S2-US-02`
- Escopo:
  - ajustar criação de TCE para `Internship` + termo inicial
  - ajustar operação de aditivo para criação de novo termo
  - alinhar payloads e respostas consumidos pelo frontend

### S2-C04 — Refatorar testes da nova modelagem no backend

- Tipo: Back-end
- História: `S2-US-03`
- Escopo:
  - atualizar testes de entidades impactadas
  - atualizar testes de services e features
  - atualizar testes de integração

### S2-C05 — Adaptar seeds para a nova estrutura de estágio

- Tipo: Back-end
- História: `S2-US-03`
- Escopo:
  - adaptar seeds ao modelo com [`Internship`](lpi-planning/01-entities/internship.md) + [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
  - garantir consistência mínima para ambientes de desenvolvimento e testes

### S2-C06 — Refatorar tipagens e contratos do frontend

- Tipo: Front-end
- História: `S2-US-04`
- Escopo:
  - adaptar tipagens ao novo modelo
  - corrigir mapeamentos afetados
  - alinhar consumo dos contratos novos

### S2-C07 — Adaptar TCE no frontend para o novo payload e resposta

- Tipo: Front-end
- História: `S2-US-04`
- Escopo:
  - ajustar submissão do TCE
  - ajustar leitura da resposta do backend
  - manter o fluxo compatível com o termo inicial

### S2-C08 — Ajustar detalhe do estágio para exibir apenas o termo vigente

- Tipo: Front-end
- História: `S2-US-04`
- Escopo:
  - exibir apenas o termo vigente na interface
  - não expor histórico de termos nesta sprint
  - corrigir renderização dos dados contratuais derivados do termo

### S2-C09 — Prototipar estrutura funcional da nova tela de detalhe

- Tipo: Front-end
- História: `S2-US-05`
- Escopo:
  - prototipar a separação entre vínculo e termo vigente
  - usar o protótipo como referência direta de implementação
  - limitar a atividade a estrutura e UX funcional da tela

## Itens dependentes de decisões posteriores

### PEND-C01 — Definir fluxo operacional de revisão contratual no produto

- Tipo: Produto + Back-end + Front-end
- Depende de: [`edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)
- Status: `PENDENTE DE DECISÃO`

### PEND-C02 — Consolidar soft delete completo em entidades restantes

- Tipo: Back-end
- Depende de: [`soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)
- Status: `PENDENTE DE DECISÃO`
