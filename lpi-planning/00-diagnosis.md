# Diagnóstico do Planejamento LPI

## Escopo deste diagnóstico

Este diagnóstico consolida o estado atual do planejamento em [`lpi-planning/`](lpi-planning) após o fechamento das decisões finais da refatoração para o modelo `Internship + InternshipTerm`.

Arquivos centrais considerados nesta consolidação:

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)
- [`lpi-planning/01-entities/supervisor.md`](lpi-planning/01-entities/supervisor.md)
- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)
- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
- [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)
- [`lpi-planning/02-flows/edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)
- [`lpi-planning/02-flows/termination-flow.md`](lpi-planning/02-flows/termination-flow.md)
- [`lpi-planning/03-cross-cutting/soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)
- [`../TERM_MODEL_REFACTOR_PLAN.md`](../TERM_MODEL_REFACTOR_PLAN.md)

O objetivo é registrar o que foi efetivamente consolidado, o que saiu do escopo da implementação atual e quais lacunas reais ainda permanecem.

## Mudanças consolidadas

### Estrutura do domínio de estágio

- `Internship` representa a identidade do vínculo entre aluno e empresa.
- `InternshipTerm` representa o estado contratual por período.
- O domínio usa modelo baseado em snapshots.
- Alterações contratuais não sobrescrevem o termo atual.
- Alterações contratuais geram novo `InternshipTerm`.
- Revisão não cria novo `type`; ela mantém `INITIAL` ou `ADDENDUM` e usa `revisedFromTermId`.

### Imutabilidade do vínculo

- `companyId` permanece fixo durante a vida do estágio.
- `studentId` também é imutável após a criação.
- Conceitualmente não existe transferência de estágio de um aluno para outro.

### Regras de fluxo entre revisão e aditivo

- Aditivo é operação do fluxo/end-point de aditivo.
- Revisão é operação do end-point de update do termo vigente.
- O critério entre revisão e aditivo é o fluxo/end-point de origem.
- O sistema não deve inferir automaticamente essa distinção a partir do conteúdo alterado.

### Rescisão

- `terminationDate` permanece em `Internship`.
- A rescisão é definitiva nesta fase.
- Não existe fluxo de reabertura nesta implementação.
- Eventual reversão futura, se existir, deverá ser tratada como fluxo específico e controlado, fora do escopo atual.

### Soft delete

- `Internship` usa `deletedAt`.
- `InternshipTerm` usa `deletedAt`.
- Perda de vigência lógica por revisão não se confunde com `deletedAt`.
- Termos revisados não devem ser deletados; apenas deixam de ser vigentes.

### Escopo da implementação atual

- `placementAgency` permanece como campo legado `string nullable` em `InternshipTerm`.
- `AgentIntegrator` não entra nesta implementação.
- Não é necessária estratégia de migração complexa de dados legados.
- Pode-se assumir reset de banco e reconstrução na nova estrutura.
- O fluxo de aditivo não entra na sprint atual.
- Nesta fase, apenas a estrutura necessária para suportar aditivo futuramente deve ser preparada.

### Contrato de leitura e compatibilidade

- O contrato principal de criação e leitura pode permanecer achatado, compatível com o modelo atual sempre que possível.
- Essa compatibilidade não altera a separação estrutural entre `Internship` e `InternshipTerm`.
- O backend pode expor um endpoint adicional de histórico: `getTermsByInternId`.
- Esse endpoint deve retornar a lista de termos ordenada temporalmente.

## Riscos e fragilidades remanescentes

### Contrato público achatado

- A compatibilidade temporária reduz impacto imediato no frontend.
- O risco remanescente é confundir shape de API com modelo interno do domínio.
- A documentação precisa continuar explícita em separar contrato principal compatível e modelagem interna nova.

### Histórico de termos

- O endpoint adicional de histórico melhora a legibilidade do modelo.
- O ponto sensível remanescente é garantir consistência entre leitura principal achatada e leitura histórica ordenada.

### Fluxo de aditivo fora de escopo da sprint

- A decisão reduz escopo da entrega atual.
- O risco remanescente é implementar a estrutura de termos de modo insuficiente para suportar `ADDENDUM` depois.
- Por isso, o tipo e a modelagem do termo já precisam nascer compatíveis com aditivo, mesmo sem fluxo entregue agora.

### `AgentIntegrator` fora desta implementação

- A decisão reduz a complexidade imediata.
- O risco remanescente é o time esquecer que `placementAgency` é apenas legado transitório e tratá-lo como solução final.

### Soft delete parcial no sistema

- `Internship` e `InternshipTerm` já estão decididos com `deletedAt`.
- Ainda existe dependência de futuras confirmações para outras entidades do sistema.
- Esse ponto continua exigindo disciplina para não generalizar prematuramente o padrão como se estivesse consolidado em todo o domínio.

## Pendências reais

Os pontos abaixo continuam sem decisão formal completa:

- `PENDENTE DE DECISÃO`: se Empresa já está oficialmente consolidada com `deletedAt`.
- `PENDENTE DE DECISÃO`: se Aluno já está oficialmente consolidado com `deletedAt`.
- `PENDENTE DE DECISÃO`: se Supervisor já está oficialmente consolidado com `deletedAt`.
- `PENDENTE DE DECISÃO`: se Usuário já está oficialmente consolidado com `deletedAt`.
- `PENDENTE DE DECISÃO`: se Curso já está oficialmente consolidado com `deletedAt`.

## Resumo do diagnóstico

- A mudança estrutural principal foi consolidada.
- As pendências centrais de `deletedAt`, imutabilidade de `studentId`, critério entre revisão e aditivo e política de reabertura deixaram de estar em aberto.
- O escopo atual foi simplificado de forma explícita: `AgentIntegrator` fica fora, `placementAgency` permanece legado, aditivo fica fora da sprint, e o contrato principal pode permanecer achatado temporariamente.
- As lacunas reais remanescentes estão concentradas principalmente na consolidação de soft delete em outras entidades do sistema.
