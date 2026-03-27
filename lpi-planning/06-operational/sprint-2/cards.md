# Cards da Sprint 2

## Blocos de execução

### S2-C01 — `Lote 0`: formalizar o novo domínio em testes de domínio

- Tipo: Back-end
- História: `S2-US-01`
- Escopo:
  - especificar invariantes de vínculo em [`Internship`](lpi-planning/01-entities/internship.md)
  - especificar invariantes de snapshot em [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
  - cobrir revisão, termo válido, termo vigente, rescisão e `deletedAt`
  - evitar dependência forte de mocks de infraestrutura nesta fase

### S2-C02 — Modelar banco, migrations e seed do novo modelo

- Tipo: Back-end
- História: `S2-US-02`
- Escopo:
  - criar a estrutura persistida de [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
  - ajustar [`Internship`](lpi-planning/01-entities/internship.md) para o recorte persistido do vínculo
  - reposicionar supervisor e `placementAgency` conforme o novo modelo
  - adaptar migrations e seed ao desenho novo

### S2-C03 — Implementar entidades e regras de domínio de `Internship` + `InternshipTerm`

- Tipo: Back-end
- História: `S2-US-02`
- Escopo:
  - separar regras de vínculo das regras contratuais
  - garantir imutabilidade de `studentId` e `companyId`
  - manter supervisor no termo
  - consolidar regras de revisão e distinção entre termo válido e termo vigente

### S2-C04 — Adaptar casos de uso de TCE e evolução contratual ao modelo de snapshots

- Tipo: Back-end
- História: `S2-US-03`
- Escopo:
  - ajustar TCE para criar vínculo + termo inicial
  - reinterpretar atualização contratual do termo vigente como operação compatível com snapshots
  - manter compatibilidade estrutural com `ADDENDUM`, sem entregar o fluxo operacional de aditivo

### S2-C05 — Implementar read model e compatibilidade temporária do contrato achatado

- Tipo: Back-end
- História: `S2-US-03`
- Escopo:
  - consolidar leitura principal baseada em vínculo + termo vigente
  - manter contrato principal compatível quando necessário para create/read principal
  - preparar leitura separada de histórico sem torná-la entrega obrigatória de UI nesta sprint

### S2-C06 — Implementar fluxo de rescisão no backend

- Tipo: Back-end
- História: `S2-US-04`
- Escopo:
  - gravar `terminationDate` em [`Internship`](lpi-planning/01-entities/internship.md)
  - encerrar o estágio de forma definitiva nesta fase
  - bloquear novos termos e revisão após rescisão
  - preservar histórico existente sem reabertura

### S2-C07 — Validar integração e regressão do backend no novo modelo

- Tipo: Back-end
- História: `S2-US-03`
- Escopo:
  - validar integração entre persistência, domínio, casos de uso e read model
  - cobrir regressões mínimas de TCE, leitura principal e rescisão
  - garantir consistência operacional do modelo novo antes de acoplar o frontend final

### S2-C08 — Adaptar contratos, tipagens e TCE do frontend ao recorte compatível da sprint

- Tipo: Front-end
- História: `S2-US-05`
- Escopo:
  - ajustar tipagens e mapeamentos afetados pela nova semântica de vínculo + termo vigente
  - adaptar submissão e leitura do TCE no contrato compatível da sprint
  - evitar qualquer tentativa de expor histórico de termos nesta fase

### S2-C09 — Prototipar a nova organização visual da tela de estágio

- Tipo: Front-end
- História: `S2-US-06`
- Escopo:
  - prototipar separação entre bloco de vínculo e bloco de termo vigente
  - prever espaço plausível para histórico futuro
  - limitar a atividade a estrutura funcional e alinhamento de UX

### S2-C10 — Reorganizar a visualização operacional do estágio com base no protótipo

- Tipo: Front-end
- História: `S2-US-06`
- Escopo:
  - aplicar a separação entre vínculo e termo vigente na tela operacional
  - alinhar a visualização ao read model estabilizado do backend
  - acomodar o estado de estágio encerrado por rescisão sem abrir histórico nem reabertura

## Itens dependentes de decisões posteriores

### PEND-C01 — Definir entrega operacional do fluxo de aditivo

- Tipo: Produto + Back-end + Front-end
- Depende de: [`amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)
- Status: `PENDENTE DE DECISÃO`

### PEND-C02 — Definir visualização de histórico de termos na UI

- Tipo: Produto + Front-end
- Depende de: [`internship-term.md`](lpi-planning/01-entities/internship-term.md)
- Status: `PENDENTE DE DECISÃO`

### PEND-C03 — Consolidar soft delete completo em entidades restantes

- Tipo: Back-end
- Depende de: [`soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)
- Status: `PENDENTE DE DECISÃO`
