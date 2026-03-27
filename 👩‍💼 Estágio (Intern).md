# 👩‍💼 Estágio (Intern)

## Propósito

`Internship` representa a identidade persistida do vínculo de estágio entre aluno e empresa.

Ele não representa mais as condições contratuais variáveis do estágio.

## Princípio central

- `Internship` = identidade do vínculo
- `InternshipTerm` = condições contratuais por período
- O modelo é baseado em snapshots: mudanças contratuais geram novos termos, sem sobrescrever histórico

## Campos

- `id`
- `studentId`
- `companyId`
- `terminationDate` (`nullable`)
- `createdAt`
- `updatedAt`
- `deletedAt` (`nullable`)

## Regras estruturais

- Cada estágio pertence a um aluno existente.
- Cada estágio pertence a uma empresa existente.
- A empresa permanece fixa durante toda a vida do estágio.
- `studentId` não pode ser alterado após a criação.
- Conceitualmente não existe transferência de estágio entre alunos.
- Se houver necessidade de mudança de empresa, o estágio atual deve ser encerrado e um novo estágio deve ser criado.
- `Internship` não deve armazenar supervisor, `placementAgency`, datas contratuais, remuneração, carga horária nem campos de aditivo.
- O estágio deve possuir ao menos um `InternshipTerm`, criado no TCE como termo inicial.

## Relação com termo de estágio

- A linha temporal contratual do estágio é formada exclusivamente pelos registros de `InternshipTerm` vinculados ao estágio.
- Todos os termos do estágio pertencem ao mesmo vínculo entre aluno e empresa.
- Não pode haver sobreposição entre termos válidos do mesmo estágio.
- Um aluno não pode manter períodos de estágio sobrepostos, mesmo quando pertençam a estágios diferentes.

## Rescisão e ciclo de vida

- `terminationDate`, quando preenchido, representa a rescisão do estágio.
- Nesta fase, a rescisão é definitiva.
- Após a rescisão, o estágio é encerrado.
- Um estágio rescindido preserva histórico.
- Um estágio rescindido não pode receber novos termos.
- Um estágio rescindido não pode receber revisão de termos.
- A exclusão lógica usa `deletedAt` sem apagar histórico.

## Invariantes

- A identidade do estágio permanece separada das condições contratuais.
- A continuidade contratual é registrada exclusivamente em `InternshipTerm`.
- A existência de termos não substitui a identidade do estágio.
- `studentId` é imutável após a criação do vínculo.
- `amendment_start_date` e `amendment_end_date` não fazem mais parte do domínio.

## Observação

- A compatibilidade temporária de contrato achatado na API não altera a separação estrutural entre vínculo e termo.
