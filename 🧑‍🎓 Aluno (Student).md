# 🧑‍🎓 Aluno (Student)

## Regras gerais

- Cada aluno tem uma matrícula única, portanto não podem existir duas iguais.
- O e-mail também é único e deve ter formato válido.

## Campos obrigatórios

- `name`
- `email`
- `phone`
- `registration`
- `admission_semester`
- `period`

## Validações

- O telefone deve seguir o padrão brasileiro `XX9YYYYYYYY`, apenas números.
- O período pode ser apenas `matutino`, `vespertino` ou `noturno`.
- O semestre de admissão deve ser um número inteiro positivo.

## Restrições

- Um aluno pode ser editado, por exemplo para alterar e-mail, telefone ou matrícula, desde que as regras de unicidade sejam mantidas.
- Um aluno não pode ser excluído se houver estágios vinculados.
