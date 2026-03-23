# 👩‍💼 Estágio (Intern)

## Estrutura e vínculo

- Cada estágio deve estar vinculado a um aluno, uma empresa e um supervisor existentes.
- O supervisor precisa pertencer à mesma empresa do estágio.

## Campos obrigatórios

- `studentId`
- `companyId`
- `supervisorId`
- `isMandatory`
- `internship_payment`
- `working_hours`
- `start_date`
- `end_date`
- `isActive`

## Campos opcionais

- `placementAgency`
- `amendment_start_date`
- `amendment_end_date`
- `termination_date`
- `meal_allowance`
- `transport_allowance`

## Validações numéricas

- Os valores numéricos `internship_payment`, `meal_allowance`, `transport_allowance` e `working_hours` devem ser positivos.
- `working_hours` não pode ultrapassar 30 horas semanais.

## Datas e coerência temporal

- A data de início (`start_date`) não pode ser futura em relação à data de criação do registro.
- A data de término (`end_date`) precisa ser posterior à data de início.
- Se o estágio for criado como ativo, `end_date` não pode estar no passado.

### Regras para termo aditivo

- `amendment_start_date` deve ser posterior a `end_date`.
- `amendment_end_date` deve ser posterior a `amendment_start_date`.

### Regras para rescisão

- `termination_date` não pode ser maior que a data atual.

### Ordem temporal esperada

```text
start_date < end_date < amendment_start_date < amendment_end_date < termination_date <= now
```

Essa sequência deve ser respeitada quando os campos existirem.

## Status e atividade

- Um aluno só pode ter um estágio ativo por vez.
- O status (`isActive`) é determinado automaticamente com base nas datas.

### Um estágio é ativo se

- `termination_date` não existe; e
- `amendment_end_date` — ou `end_date`, se não houver aditivo — ainda não passou.

### Um estágio é finalizado se

- `termination_date` existe e é anterior à data atual; ou
- `amendment_end_date`, se existir, é anterior à data atual; ou
- `end_date` é anterior à data atual.

### Comportamento automático

- A atualização de status é automática, conforme a data atual do sistema.
- Se um estágio atender aos critérios de término, mas ainda estiver marcado como ativo, o sistema deve corrigi-lo automaticamente.

## Restrições adicionais

- Um estágio não pode ter períodos sobrepostos com outro estágio, ativo ou inativo, do mesmo aluno.
- Exemplo: um estágio que vai de janeiro a junho impede outro estágio do mesmo aluno que comece em março.
- Não é permitido alterar aluno, empresa ou supervisor de um estágio já iniciado (`start_date <= now`).
- Futuramente, poderá ser possível substituir o supervisor se o novo pertencer à mesma empresa.

## Campos informativos

- O campo `isMandatory` indica se o estágio é obrigatório, no sentido acadêmico.
- Atualmente, ele não altera o comportamento do sistema, mas poderá influenciar requisitos como horas mínimas ou presença de agente de integração.

## Exclusão

- Só é permitido deletar o estágio se a data atual for maior que `end_date`, `amendment_end_date` e `termination_date`.
- Só é permitido deletar o estágio se o usuário for `SUPERUSER`.
