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

- Um supervisor não pode ser excluído se estiver vinculado a qualquer estágio.
- Um supervisor não pode mudar de empresa (`companyId`) se estiver vinculado a estágios ativos.
- Futuramente, poderá ser possível trocar o supervisor por outro da mesma empresa em um estágio em andamento.
