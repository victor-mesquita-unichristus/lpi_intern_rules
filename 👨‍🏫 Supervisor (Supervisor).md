# 👨‍🏫 Supervisor (Supervisor)

## Regras gerais

- Todo supervisor precisa estar associado a uma empresa existente.

## Campos obrigatórios

- `name`
- `companyId`

## Campos opcionais

- `phone`
- `email`

## Validações

- Se o e-mail for informado, ele deve ser único e válido.
- O telefone, se informado, deve seguir o padrão brasileiro `XX9YYYYYYYY`.

## Restrições

- Um supervisor não pode ser excluído se estiver vinculado a qualquer `InternshipTerm`.
- Um supervisor não pode mudar de empresa (`companyId`) se isso quebrar a coerência com termos de estágio já vinculados.
- O supervisor pertence ao termo, não ao estágio.
- Mudanças de supervisor em um estágio devem ocorrer por fluxo sobre o termo, e não por mutação direta de `Internship`.
