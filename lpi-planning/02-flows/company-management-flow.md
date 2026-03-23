# Fluxo de Gerenciamento de Empresa

## Objetivo do fluxo

Operar cadastro, edição, listagem e exclusão de empresas em telas administrativas.

## Entidades afetadas

- Empresa

## Campos alterados

- Campos cadastrais da empresa

## Pré-condições

- O usuário deve ter permissão para gerenciar empresas.

## Regras específicas do fluxo

- Este fluxo usa as regras de negócio definidas em [`company.md`](lpi-planning/01-entities/company.md).
- Cadastro, edição, listagem e exclusão são tratados como variantes operacionais sobre a mesma entidade.
- Tentativas de exclusão devem respeitar as proteções de relacionamento já definidas na entidade.

## Pós-condições

- Os dados da empresa são criados, atualizados, listados ou removidos de acordo com a operação solicitada.

## Comportamento esperado na UI

- A UI deve oferecer formulários administrativos para cadastro e edição.
- Telas de listagem devem permitir navegação em resultados paginados.
- Ações de exclusão devem apresentar motivos claros de bloqueio quando relacionamentos impedirem a remoção.

## Fora de escopo

- Gerenciar supervisores a partir do formulário da empresa.
- Gerenciar estágios a partir do formulário da empresa.
