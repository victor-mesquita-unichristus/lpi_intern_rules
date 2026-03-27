# Diagnóstico do Planejamento LPI

## Escopo deste diagnóstico

Este diagnóstico audita a consistência do planejamento em [`lpi-planning/`](lpi-planning) após a adoção da nova modelagem oficial de domínio.

Arquivos centrais revisados nesta consolidação:

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)
- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)
- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
- [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)
- [`lpi-planning/02-flows/edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)
- [`lpi-planning/02-flows/termination-flow.md`](lpi-planning/02-flows/termination-flow.md)
- [`lpi-planning/03-cross-cutting/soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)
- [`lpi-planning/06-operational/stories.md`](lpi-planning/06-operational/stories.md)
- [`lpi-planning/06-operational/cards.md`](lpi-planning/06-operational/cards.md)
- [`lpi-planning/06-operational/sprints.md`](lpi-planning/06-operational/sprints.md)
- [`lpi-planning/06-operational/team-allocation.md`](lpi-planning/06-operational/team-allocation.md)

O objetivo é identificar o que foi consolidado, o que ainda apresenta fragilidade de interpretação e o que permanece sem decisão formal.

## Mudanças consolidadas

### Estrutura do domínio de estágio

- `Internship` continua sendo a entidade principal do sistema.
- `Internship` representa a identidade do vínculo entre aluno e empresa.
- `terminationDate` permanece em `Internship` como parte do ciclo de vida do estágio.
- `InternshipTerm` passa a representar as condições contratuais por período.
- Supervisor e agente integrador pertencem ao termo, não ao estágio.
- Dados contratuais não devem mais existir diretamente em `Internship`.
- O domínio agora é baseado em snapshots.
- Alterações de condição não sobrescrevem o termo atual.
- Alterações de condição devem gerar novo `InternshipTerm`.
- Revisão de termo não cria novo `type`; mantém `INITIAL` ou `ADDENDUM` e usa `revisedFromTermId` como vínculo de revisão.

### Remoção do modelo antigo de aditivo em `Internship`

- `amendment_start_date` e `amendment_end_date` deixaram de fazer parte do modelo consolidado.
- Aditivo agora é documentado como criação de novo `InternshipTerm` com `type = ADDENDUM`.

### Reposicionamento de supervisor e agente integrador

- O supervisor pertence a `InternshipTerm`.
- A regra válida é: o supervisor do termo deve pertencer à empresa do estágio.
- O agente integrador pertence a `InternshipTerm`.
- Continua proibido texto livre.
- Histórico deve ser preservado mesmo se o integrador ficar inativo.

### Reposicionamento dos fluxos principais

- TCE não é entidade persistida separada.
- TCE cria um `Internship` e um `InternshipTerm` inicial.
- Edição contratual não sobrescreve termo existente.
- Edição contratual deve gerar novo snapshot em `InternshipTerm`.
- Mudança de empresa não é edição do estágio; exige encerramento e criação de outro estágio.
- Rescisão em `Internship` impede criação e revisão de termos.

### Material operacional futuro ajustado ao modelo novo

- A Sprint 2 e o planejamento posterior já podem refletir a modelagem com [`InternshipTerm`](lpi-planning/01-entities/internship-term.md).
- A Sprint 1 foi preservada como registro histórico do escopo original e não deve ser lida como reescrita retroativa do novo modelo.

## Riscos e fragilidades remanescentes

### [`tce-flow.md`](lpi-planning/02-flows/tce-flow.md)

- O enquadramento atual está correto, mas depende de leitura disciplinada em conjunto com [`internship.md`](lpi-planning/01-entities/internship.md) e [`internship-term.md`](lpi-planning/01-entities/internship-term.md).
- Se o time tratar o fluxo como fonte primária de regra temporal, há risco de voltar a misturar entidade e fluxo.

### [`amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)

- O fluxo já está alinhado ao modelo de snapshot.
- Ainda existe risco de implementação confundir aditivo formal com edição contratual genérica, porque ambos agora geram novos termos.
- Esse risco aumentou com a introdução de `revisedFromTermId`, porque a distinção entre revisão e aditivo depende de disciplina de fluxo, não de um novo `type`.

### [`edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)

- O enquadramento está mais correto, mas continua sensível a interpretação.
- Sem definição operacional mais precisa, o time pode divergir sobre quando criar novo termo com o mesmo `type` e quando tratar a mudança como aditivo formal.
- Também permanece sensível a erro de leitura sobre elegibilidade de revisão, porque a revisão só é permitida para o termo vigente.

### [`termination-flow.md`](lpi-planning/02-flows/termination-flow.md)

- A regra central está clara.
- Ainda há fragilidade caso implementação ou planejamento futuro tentem introduzir reabertura sem decisão formal, porque isso impactaria fluxo, invariantes e histórico.

### [`soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)

- A direção transversal ficou mais clara.
- O ponto frágil remanescente é a baixa confirmação formal por entidade, o que ainda exige cuidado para não transformar direção em verdade implementada.

### [`internship-term.md`](lpi-planning/01-entities/internship-term.md)

- O modelo de revisão ficou mais preciso com `revisedFromTermId`.
- Ainda existe fragilidade de interpretação operacional sobre o que conta como termo válido em consultas e validações, porque isso depende da leitura conjunta de soft delete e substituição por revisão.

### Artefatos operacionais

- O principal risco anterior era reescrever retroativamente a Sprint 1 com a modelagem nova.
- Esse risco foi corrigido, mas precisa continuar explícito para evitar novas retrointerpretações do histórico do projeto.
- O material operacional agora exige leitura temporal: Sprint 1 como registro histórico; Sprint 2 em diante como planejamento já influenciado pelo modelo novo.

## Pendências reais

Os pontos abaixo continuam sem decisão formal completa:

- `PENDENTE DE DECISÃO`: se `Internship` já usa oficialmente `deletedAt` no modelo persistido.
- `PENDENTE DE DECISÃO`: se `InternshipTerm` já usa oficialmente `deletedAt` no modelo persistido.
- `PENDENTE DE DECISÃO`: se Empresa, Aluno, Supervisor, Usuário e Curso já estão consolidados com `deletedAt`.
- `PENDENTE DE DECISÃO`: se `studentId` pode ou não ser alterado após a criação de `Internship`.
- `PENDENTE DE DECISÃO`: qual é o critério operacional para decidir quando uma alteração contratual fora do aditivo formal mantém o mesmo `type` no novo snapshot.
- `PENDENTE DE DECISÃO`: se existe política oficial de reabertura após rescisão.
- `PENDENTE DE DECISÃO`: se a revisão de termo exigirá justificativa obrigatória em versões futuras ou permanecerá opcional.

## Resumo do diagnóstico

- A mudança estrutural principal foi consolidada.
- O risco restante não está mais na direção do modelo, mas na disciplina de interpretação entre histórico do projeto, regras de entidade e fluxos operacionais.
- As maiores fragilidades remanescentes estão em soft delete, edição contratual fora do aditivo formal e eventual política de reabertura após rescisão.
