# Histórias da Sprint 2

## Histórias operacionais

### S2-US-01 — Formalizar o novo domínio de estágio em testes de domínio

Como time de engenharia, precisamos transformar as regras do novo modelo em especificação executável para reduzir ambiguidade antes de alterar banco, entidades, casos de uso e integração.

**Critérios de aceite**

- Existe uma suíte inicial de testes cobrindo invariantes de [`Internship`](lpi-planning/01-entities/internship.md) e [`InternshipTerm`](lpi-planning/01-entities/internship-term.md).
- A suíte cobre separação entre vínculo e termo, revisão por snapshot, termo válido vs termo vigente e rescisão.
- A suíte cobre bloqueio pós-rescisão para novos termos e revisões.
- A suíte não depende majoritariamente de mocks de infraestrutura.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)
- [`lpi-planning/02-flows/termination-flow.md`](lpi-planning/02-flows/termination-flow.md)

### S2-US-02 — Refatorar persistência e entidades para `Internship` + `InternshipTerm`

Como time de engenharia, precisamos migrar a base estrutural do estágio para o modelo novo para que vínculo e estado contratual deixem de compartilhar a mesma fonte de verdade persistida.

**Critérios de aceite**

- A estrutura persistida de [`InternshipTerm`](lpi-planning/01-entities/internship-term.md) existe e se relaciona corretamente com [`Internship`](lpi-planning/01-entities/internship.md).
- O backend deixa de depender operacionalmente dos campos contratuais antigos em [`Internship`](lpi-planning/01-entities/internship.md).
- Supervisor passa a ser lido e escrito no termo.
- `placementAgency` permanece apenas como legado transitório.
- Banco, migrations e seed refletem o novo modelo.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)

### S2-US-03 — Adaptar casos de uso, leitura e contratos ao modelo de snapshots

Como time de engenharia, precisamos adaptar os fluxos operacionais de estágio para que TCE, leitura principal e compatibilidade contratual funcionem com vínculo + termo vigente, preservando espaço estrutural para `ADDENDUM` sem entregar o fluxo operacional de aditivo nesta sprint.

**Critérios de aceite**

- TCE cria vínculo + termo inicial de forma consistente.
- Casos de uso e serviços impactados operam com [`Internship`](lpi-planning/01-entities/internship.md) + [`InternshipTerm`](lpi-planning/01-entities/internship-term.md).
- A leitura operacional do estágio usa vínculo + termo vigente.
- O contrato principal pode permanecer achatado temporariamente sem recolocar o modelo monolítico como fonte de verdade.
- A estrutura continua compatível com termos do tipo `ADDENDUM`, sem entregar o fluxo operacional de aditivo.

**Dependências**

- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
- [`lpi-planning/02-flows/edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)
- [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)

### S2-US-04 — Implementar o fluxo de rescisão alinhado ao novo domínio

Como time de backend, precisamos implementar a rescisão como regra permanente do vínculo para que o estágio possa ser encerrado sem quebrar o modelo novo nem preservar comportamentos indevidos do modelo antigo.

**Critérios de aceite**

- A rescisão grava `terminationDate` em [`Internship`](lpi-planning/01-entities/internship.md).
- A rescisão encerra o estágio de forma definitiva nesta fase.
- Após a rescisão, o estágio não recebe novos termos.
- Após a rescisão, o estágio não recebe revisão de termos.
- O fluxo não remove nem reescreve termos históricos.
- Não existe reabertura nesta sprint.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/02-flows/termination-flow.md`](lpi-planning/02-flows/termination-flow.md)

### S2-US-05 — Adaptar contratos operacionais do frontend ao novo recorte da sprint

Como time de frontend, precisamos adaptar tipagens, contratos e consumo dos fluxos principais para que a interface continue funcional com vínculo + termo vigente durante a fase de compatibilidade temporária.

**Critérios de aceite**

- O frontend consome o payload e a resposta do TCE no recorte compatível da sprint.
- O detalhe do estágio passa a depender de vínculo + termo vigente, mesmo quando o contrato principal permanecer achatado.
- Tipagens e mapeamentos afetados pela nova modelagem são corrigidos.
- A interface não tenta expor histórico de termos nesta sprint.

**Dependências**

- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)

### S2-US-06 — Prototipar e reorganizar a visualização de estágio para vínculo + termo vigente

Como time de frontend, precisamos validar e aplicar uma nova organização visual para que a tela de estágio deixe de apresentar dados monolíticos e passe a refletir o novo domínio.

**Critérios de aceite**

- Existe um protótipo funcional da nova organização visual da tela.
- A tela separa dados do vínculo e dados do termo vigente.
- A estrutura visual prevê espaço plausível para histórico futuro, sem exibi-lo agora.
- O protótipo é usado como referência direta de reorganização da tela ainda nesta sprint.
- A atividade permanece limitada a alinhamento estrutural e UX funcional, sem abrir uma fase paralela de refinamento estético final.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)
