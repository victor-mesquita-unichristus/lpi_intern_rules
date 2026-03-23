# Supervisor

## Propósito

Representa a pessoa da empresa responsável por supervisionar o estágio.

## Campos relevantes

- `name`
- `companyId`
- `phone`
- `email`

## Regras de cadastro

- `name` e `companyId` são obrigatórios.
- A empresa referenciada deve existir.
- Se informado, `email` deve ser único e válido.
- Se informado, `phone` deve seguir o formato brasileiro `XX9YYYYYYYY`.

## Regras de edição

- Os dados do supervisor podem ser editados desde que as regras de validação continuem válidas.
- `companyId` não pode ser alterado se o supervisor estiver vinculado a estágios ativos.

## Regras de exclusão

- Um supervisor não pode ser excluído se estiver vinculado a qualquer estágio.

## Relacionamentos

- Muitos supervisores pertencem a uma empresa.
- Um supervisor pode supervisionar muitos estágios.

## Invariantes

- Todo supervisor pertence a uma empresa existente.
- Um supervisor usado em um estágio deve pertencer à mesma empresa do estágio.

## Observações de MVP

- A substituição de supervisor durante um estágio em andamento está fora do escopo atual do MVP.
