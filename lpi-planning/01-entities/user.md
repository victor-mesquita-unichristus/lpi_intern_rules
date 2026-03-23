# Usuário

## Propósito

Representa um ator autenticado no sistema.

## Campos relevantes

- `name`
- `email`
- `password`
- `role`

## Regras de cadastro

- `name`, `email`, `password` e `role` são obrigatórios.
- `email` deve ser único e válido.
- `password` deve ter no mínimo 8 caracteres.
- `password` deve conter pelo menos 1 letra e 1 número.
- Senhas devem ser armazenadas com hash.

## Regras de edição

- Dados do usuário podem ser editados desde que a unicidade do email seja preservada.
- Apenas administradores e superusuários podem alterar o `role` de outro usuário.

## Regras de exclusão

- O comportamento de exclusão é controlado pelas regras de autorização e fica reservado para usuários privilegiados.

## Relacionamentos

- As permissões do usuário dependem do `role` atribuído.

## Invariantes

- Todo usuário possui exatamente um `role` válido.
- Credenciais nunca são armazenadas em texto puro.

## Observações de MVP

- Autogestão de conta está fora do escopo do MVP.
