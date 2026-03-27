# Termo de Estágio

## Propósito

`InternshipTerm` representa as condições contratuais do estágio ao longo do tempo.

O modelo é baseado em snapshots:

- o histórico é imutável
- cada termo representa um recorte contratual válido por período
- alterações contratuais geram novos termos, e não sobrescrita do termo atual

## Princípio central

- `Internship` representa a identidade do vínculo.
- `InternshipTerm` representa as condições contratuais por período.

## Campos

- `id`
- `internshipId`
- `type` (`INITIAL | ADDENDUM`)
- `revisedFromTermId` (`nullable`)
- `startDate`
- `endDate`
- `supervisorId`
- `internshipPayment`
- `workingHours`
- `mealAllowance` (`nullable`)
- `transportAllowance` (`nullable`)
- `isMandatory`
- `agentIntegratorId` (`nullable`)
- `createdAt`
- `updatedAt`
- `deletedAt` (`PENDENTE DE DECISÃO`: confirmar se o padrão global já está consolidado para esta entidade)

## Regras de criação

- Todo termo pertence a um `Internship` existente.
- `type` deve ser `INITIAL` ou `ADDENDUM`.
- Revisão não é um novo `type`.
- O supervisor pertence ao termo, não ao estágio.
- O supervisor informado deve pertencer à empresa do estágio associado.
- `agentIntegratorId` é opcional.
- Quando informado, `agentIntegratorId` deve referenciar um agente integrador existente e ativo.
- O agente integrador nunca deve ser informado por texto livre.

## Regras temporais

- O termo inicial define o primeiro período contratual do estágio.
- Cada novo termo válido deve respeitar a linha temporal do estágio.
- Não pode haver sobreposição entre termos válidos do mesmo estágio.
- Após o preenchimento de `terminationDate` em `Internship`, não podem ser criados novos termos.

## Leitura operacional de termos válidos

Para efeito de validação e leitura operacional, considerar como válidos os termos que:

- não estejam removidos logicamente; e
- não tenham sido substituídos por um termo de revisão posterior.

`createdAt` não define cronologia de negócio. A coerência temporal deve ser analisada com base em `startDate`, `endDate` e no conjunto de termos válidos do mesmo estágio.

## Definição de termo vigente

- Termo vigente é o termo válido mais recente na linha temporal do estágio.
- Termo vigente não se confunde com termo válido: pode existir mais de um termo válido no histórico, mas apenas um termo vigente por estágio em cada momento de leitura operacional.

## Regra de snapshot

- Qualquer alteração nas condições do estágio não edita o termo atual.
- Qualquer alteração nas condições do estágio deve gerar um novo `InternshipTerm`.
- O novo termo pode manter o mesmo `type`, quando aplicável.
- O histórico de termos deve permanecer imutável.

## Regra de revisão

- Quando um termo precisar ser corrigido ou revisado, o sistema não sobrescreve o termo atual.
- O sistema cria um novo `InternshipTerm`.
- O novo termo mantém o mesmo `type` do termo revisado.
- O novo termo preenche `revisedFromTermId` com o identificador do termo anterior.
- `revisedFromTermId` representa vínculo de revisão entre snapshots e não ordem cronológica geral do estágio.
- A cadeia de revisão sempre recai sobre o termo vigente.
- Quando um termo é revisado, ele deixa de ser vigente e permanece apenas como histórico.

## Permissão e elegibilidade de revisão

- Qualquer usuário com permissão de edição do fluxo pode revisar o termo.
- Um termo só pode ser revisado enquanto for o termo vigente do estágio.
- Se já existir outro termo válido posterior, o termo anterior deixa de ser vigente e não pode mais ser revisado.
- Revisões sucessivas formam uma cadeia sobre o termo vigente mais recente, e não sobre termos históricos já substituídos.
- Após o preenchimento de `terminationDate` em `Internship`, não pode haver revisão de termos.
- Justificativa de revisão é desejável, mas não obrigatória no MVP.

## Regras de revisão por tipo

- Revisão de termo `INITIAL` gera novo termo com `type = INITIAL`.
- Revisão de termo `ADDENDUM` gera novo termo com `type = ADDENDUM`.
- Ao revisar um termo `INITIAL`, `startDate` e `endDate` podem ser ajustados, desde que a linha temporal do estágio seja preservada e não haja sobreposição com termos válidos posteriores.
- Ao revisar um termo `ADDENDUM`, `startDate` e `endDate` podem ser ajustados, desde que a sequência temporal do estágio seja preservada e não haja sobreposição com outros termos válidos.

## Regras por tipo

- TCE cria um `InternshipTerm` com `type = INITIAL`.
- Aditivo cria um `InternshipTerm` com `type = ADDENDUM`.

## Relacionamentos

- Um termo pertence a um estágio.
- Um termo pertence a um supervisor.
- Um termo pode ter zero ou um agente integrador associado.

## Observações

- Esta entidade substitui completamente o uso de `amendment_start_date` e `amendment_end_date` no domínio.
- Campos contratuais não devem mais existir diretamente em `Internship`.
