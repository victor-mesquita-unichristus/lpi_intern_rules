# Estágio

## Propósito

Representa a entidade persistida central do sistema LPI.

No MVP, o próprio estágio é a formalização do TCE dentro do sistema. Não existe uma entidade persistida separada para TCE.

## Campos relevantes

- `studentId`
- `companyId`
- `supervisorId`
- `agentIntegratorId`
- `isMandatory`
- `internship_payment`
- `working_hours`
- `start_date`
- `end_date`
- `amendment_start_date`
- `amendment_end_date`
- `termination_date`
- `meal_allowance`
- `transport_allowance`
- `isActive`

## Regras de cadastro

- `studentId`, `companyId`, `supervisorId`, `isMandatory`, `internship_payment`, `working_hours`, `start_date` e `end_date` são obrigatórios.
- Aluno, empresa e supervisor devem existir.
- O supervisor deve pertencer à mesma empresa do estágio.
- `agentIntegratorId` é opcional, mas, se informado, deve referenciar um agente integrador existente e ativo.
- Valores numéricos devem ser positivos.
- `working_hours` não pode ultrapassar 30 horas semanais.
- `start_date` não pode ser futura no momento do cadastro.
- `end_date` deve ser posterior a `start_date`.
- Se o estágio for criado como ativo, `end_date` não pode estar no passado.

## Regras de edição

- Os dados do estágio podem ser editados apenas dentro das restrições de negócio permitidas.
- `studentId`, `companyId` e `supervisorId` não podem ser alterados após o início do estágio.
- Campos de aditivo e rescisão seguem fluxos operacionais próprios.
- `PENDENTE DE DECISÃO`: quais campos-base do estágio podem ser alterados antes do início, especialmente empresa e supervisor.

## Regras de exclusão

- A exclusão só é permitida depois que todas as datas finais relevantes já tiverem passado.
- A exclusão só é permitida para `SUPERUSER`.
- A direção do sistema é alinhar a exclusão ao soft delete global com `deletedAt` sempre que possível.
- `PENDENTE DE DECISÃO`: se `Estágio` já usa oficialmente `deletedAt` no modelo persistido ou se isso ainda é apenas um alvo de consolidação.

## Relacionamentos

- Um estágio pertence a um aluno.
- Um estágio pertence a uma empresa.
- Um estágio pertence a um supervisor.
- Um estágio pode pertencer opcionalmente a um agente integrador.

## Invariantes

- O supervisor sempre pertence à empresa do estágio.
- Um aluno não pode ter períodos de estágio sobrepostos.
- Um aluno pode ter apenas um estágio ativo por vez.
- A coerência temporal deve ser preservada entre datas-base, datas de aditivo e data de rescisão.
- Quando existirem, a ordem temporal esperada é `start_date < end_date < amendment_start_date < amendment_end_date < termination_date <= now`.
- `termination_date` não pode ser maior que a data atual.
- `isActive` é determinado pelas datas do estágio e pelo estado de rescisão.

## Observações de MVP

- `isMandatory` é informativo no MVP e ainda não altera o comportamento dos fluxos.
- Aditivo e rescisão existem como fluxos operacionais dedicados, mas as regras de coerência temporal pertencem à verdade de domínio desta entidade.
- Não existem entidades persistidas separadas para TCE, aditivo ou rescisão no MVP. Esses são fluxos operacionais sobre `Estágio`.
