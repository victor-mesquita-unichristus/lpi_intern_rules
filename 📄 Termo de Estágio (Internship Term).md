# 📄 Termo de Estágio (Internship Term)

## Propósito

`InternshipTerm` representa as condições contratuais de um estágio em um período específico.

O modelo é baseado em snapshots:

- o histórico é imutável
- cada termo representa um recorte contratual válido por período
- alterações contratuais geram novos termos, sem sobrescrever o termo anterior

## Princípio central

- `Internship` representa a identidade do vínculo
- `InternshipTerm` representa as condições contratuais por período

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
- `placementAgency` (`nullable`, legado)
- `createdAt`
- `updatedAt`
- `deletedAt` (`nullable`)

## Regras de criação

- Todo termo pertence a um `Internship` existente.
- `type` deve ser `INITIAL` ou `ADDENDUM`.
- Revisão não é um novo `type`.
- O supervisor pertence ao termo, não ao estágio.
- O supervisor informado deve pertencer à empresa do estágio associado.
- `placementAgency` é opcional e permanece como campo legado `string nullable` nesta fase.
- `AgentIntegrator` não entra nesta implementação.

## Regras temporais

- O termo inicial define o primeiro período contratual do estágio.
- Cada novo termo válido deve respeitar a linha temporal do estágio.
- Não pode haver sobreposição entre termos válidos do mesmo estágio.
- Após o preenchimento de `terminationDate` em `Internship`, não podem ser criados novos termos.

## Termos válidos e termo vigente

Para leitura operacional, considerar como válidos os termos que:

- não estejam removidos logicamente
- não tenham sido substituídos por um termo de revisão posterior

Regras adicionais:

- `createdAt` não define cronologia de negócio.
- A coerência temporal deve ser analisada com base em `startDate`, `endDate` e no conjunto de termos válidos do mesmo estágio.
- Termo vigente é o termo válido mais recente na linha temporal do estágio.
- Pode existir mais de um termo válido no histórico, mas apenas um termo vigente por estágio em cada momento de leitura operacional.

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
- Termos revisados não devem ser deletados; eles apenas perdem vigência lógica.

## Permissão e elegibilidade de revisão

- Um termo só pode ser revisado enquanto for o termo vigente do estágio.
- Se já existir outro termo válido posterior, o termo anterior deixa de ser vigente e não pode mais ser revisado.
- Revisões sucessivas formam uma cadeia sobre o termo vigente mais recente, e não sobre termos históricos já substituídos.
- Após o preenchimento de `terminationDate` em `Internship`, não pode haver revisão de termos.
- Justificativa de revisão é desejável, mas não obrigatória no MVP.

## Regras por tipo

- TCE cria um `InternshipTerm` com `type = INITIAL`.
- O endpoint de aditivo cria um `InternshipTerm` com `type = ADDENDUM`.
- O endpoint de update do termo vigente cria revisão e mantém o `type` do termo revisado.
- O critério entre aditivo e revisão é o fluxo/end-point de origem, e não inferência automática.
- Revisão de termo `INITIAL` gera novo termo com `type = INITIAL`.
- Revisão de termo `ADDENDUM` gera novo termo com `type = ADDENDUM`.
- Ao revisar um termo `INITIAL`, `startDate` e `endDate` podem ser ajustados, desde que a linha temporal do estágio seja preservada e não haja sobreposição com termos válidos posteriores.
- Ao revisar um termo `ADDENDUM`, `startDate` e `endDate` podem ser ajustados, desde que a sequência temporal do estágio seja preservada e não haja sobreposição com outros termos válidos.

## Relacionamentos

- Um termo pertence a um estágio.
- Um termo pertence a um supervisor.
- Um termo pode armazenar `placementAgency` legado como dado contratual opcional nesta fase.

## Observações

- Esta entidade substitui completamente o uso de `amendment_start_date` e `amendment_end_date` no domínio.
- Campos contratuais não devem mais existir diretamente em `Internship`.
- O tipo `ADDENDUM` permanece no modelo mesmo quando o fluxo correspondente estiver fora do escopo da sprint atual.
