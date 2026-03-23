# Aluno

## Propósito

Representa o aluno matriculado em um curso e elegível para estágios.

## Campos relevantes

- `name`
- `email`
- `phone`
- `registration`
- `admission_semester`
- `period`
- `courseId`

## Regras de cadastro

- `name`, `email`, `phone`, `registration`, `admission_semester` e `period` são obrigatórios.
- `registration` deve ser único.
- `email` deve ser único e válido.
- `phone` deve conter apenas dígitos e seguir `XX9YYYYYYYY`.
- `period` aceita apenas `matutino`, `vespertino` ou `noturno`.
- `admission_semester` deve ser um inteiro positivo.
- `courseId` deve referenciar um curso existente e ativo.

## Regras de edição

- Os dados do aluno podem ser editados desde que as regras de unicidade e formato sejam preservadas.
- A mudança de curso deve sempre apontar para um curso existente e ativo.

## Regras de exclusão

- Um aluno não pode ser excluído se houver estágios vinculados ao aluno.

## Relacionamentos

- Todo aluno pertence a um curso ativo.
- Um aluno pode ter múltiplos estágios ao longo do tempo.

## Invariantes

- A matrícula do aluno é única.
- O email do aluno é único.
- Períodos de estágio do mesmo aluno não podem se sobrepor.

## Observações de MVP

- Complexidades do ciclo de vida do aluno além da proteção por estágio vinculado estão fora do escopo do MVP.
