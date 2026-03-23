# 👤 Usuário (User)

## Campos obrigatórios

- `name`
- `email`
- `password`
- `role`

## Regras de validação

- O e-mail é único e deve ser válido.
- A senha deve ter no mínimo 8 caracteres, contendo pelo menos 1 número e 1 letra.
- A senha deve ser armazenada de forma segura, com hash, e nunca em texto puro.

## Valores permitidos para `role`

- `SUPERUSER`
- `ADMIN`
- `COMMON`

## Permissões por papel

- `COMMON`: pode apenas visualizar (`read`) registros.
- `ADMIN`: pode visualizar, criar e editar registros.
- `SUPERUSER`: tem acesso total, inclusive para excluir registros e gerenciar permissões.

## Restrições

- Apenas administradores ou superusuários podem alterar o campo `role` de outros usuários.
- Usuários podem editar o próprio e-mail e senha, mas isso fica fora do escopo do MVP e está planejado para versão futura.
