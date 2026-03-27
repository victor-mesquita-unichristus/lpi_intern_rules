# Supervisor

## Propósito

Representa a pessoa da empresa responsável por supervisionar termos de estágio.

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
- `companyId` não pode ser alterado se isso quebrar a coerência entre o supervisor e termos de estágio aos quais ele já esteja vinculado.

## Regras de exclusão

- Um supervisor não pode ser excluído se estiver vinculado a qualquer `InternshipTerm`.

## Relacionamentos

- Muitos supervisores pertencem a uma empresa.
- Um supervisor pode supervisionar muitos termos de estágio.

## Invariantes

- Todo supervisor pertence a uma empresa existente.
- Um supervisor usado em um `InternshipTerm` deve pertencer à mesma empresa do `Internship` associado.
- Mudança de supervisor em um estágio não ocorre por mutação direta de `Internship`; ela ocorre por fluxo sobre o termo.

## Observações de MVP

- Nesta fase, o sistema continua validando supervisor por empresa nos fluxos que criam ou revisam termos.
