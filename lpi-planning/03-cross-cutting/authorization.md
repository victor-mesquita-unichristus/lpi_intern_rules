# Authorization

## Propósito

Definir o controle de acesso baseado em papéis para todos os fluxos.

## Papéis

- `COMMON`
- `ADMIN`
- `SUPERUSER`

## Regras

- `COMMON` pode apenas visualizar dados.
- `ADMIN` pode criar e editar registros.
- `SUPERUSER` pode criar, editar, excluir e gerenciar permissões.
- Ações sensíveis, como exclusão, devem ser protegidas explicitamente.
- Alterar o papel de outro usuário é uma ação limitada a usuários com nível administrativo.
