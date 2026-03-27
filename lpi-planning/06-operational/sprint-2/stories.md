# Histórias da Sprint 2

## Histórias operacionais

### S2-US-01 — Refatorar a persistência do estágio para `Internship` + `InternshipTerm`

Como time de engenharia, precisamos migrar a persistência do estágio para o modelo novo para que a base de dados e os fluxos deixem de depender do modelo contratual antigo em [`Internship`](lpi-planning/01-entities/internship.md).

**Critérios de aceite**

- A estrutura persistida de [`InternshipTerm`](lpi-planning/01-entities/internship-term.md) existe e está integrada ao fluxo de estágio.
- O backend deixa de depender operacionalmente dos campos contratuais antigos em [`Internship`](lpi-planning/01-entities/internship.md).
- Supervisor passa a ser lido e escrito no termo.
- As migrações necessárias estão definidas.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)

### S2-US-02 — Refatorar domínio, casos de uso e leitura do termo vigente

Como time de engenharia, precisamos adaptar o domínio e os casos de uso de estágio para que o sistema opere corretamente com snapshots contratuais e leitura do termo vigente, preservando compatibilidade estrutural com `ADDENDUM` sem entregar o fluxo operacional de aditivo nesta sprint.

**Critérios de aceite**

- Casos de uso e services impactados passam a operar com [`Internship`](lpi-planning/01-entities/internship.md) + [`InternshipTerm`](lpi-planning/01-entities/internship-term.md).
- A leitura operacional de estágio considera apenas o termo vigente quando necessário para resposta do sistema.
- O fluxo de TCE cria estágio e termo inicial de forma consistente.
- A estrutura do domínio e dos contratos permanece compatível com termos do tipo `ADDENDUM`, sem entregar o fluxo operacional de aditivo nesta sprint.

**Dependências**

- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
- [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)
- [`lpi-planning/02-flows/edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)

### S2-US-03 — Refatorar testes e seeds para a nova modelagem

Como time de engenharia, precisamos adaptar testes e seeds para que a nova modelagem tenha cobertura e ambiente consistente de execução.

**Critérios de aceite**

- Testes de entidades impactadas são atualizados.
- Testes de services, features e integração são atualizados.
- Seeds passam a refletir o modelo com termo de estágio.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)

### S2-US-04 — Adaptar contratos e fluxos do frontend ao termo vigente

Como time de frontend, precisamos adaptar contratos, tipagens e telas para que a interface continue funcional no modelo novo sem expor histórico de termos.

**Critérios de aceite**

- O frontend consome o novo payload e resposta do TCE.
- O detalhe do estágio exibe apenas o termo vigente.
- A tela separa dados do vínculo e dados do termo vigente.
- A estrutura visual fica preparada para histórico futuro sem expor histórico nesta sprint.
- Tipagens e mapeamentos afetados pela nova modelagem são corrigidos.
- A interface não tenta exibir histórico de termos nesta sprint.

### S2-US-05 — Prototipar e consolidar a nova estrutura visual do detalhe do estágio

Como time de frontend, precisamos validar rapidamente a estrutura visual da nova tela para reduzir retrabalho durante a implementação da separação entre vínculo e termo vigente.

**Critérios de aceite**

- Existe um protótipo funcional da estrutura da tela de detalhe.
- O protótipo é usado como referência direta de implementação ainda nesta sprint.
- A atividade permanece limitada a alinhamento estrutural e UX da tela, sem abrir uma fase paralela de refinamento estético.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)

**Dependências**

- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)
- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
