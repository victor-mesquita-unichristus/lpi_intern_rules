# Fluxo de Gerenciamento de Supervisor

## Objetivo do fluxo

Operar cadastro, edição, listagem e exclusão de supervisores em telas administrativas.

## Entidades afetadas

- Supervisor
- Empresa

## Campos alterados

- Campos cadastrais do supervisor
- `companyId`

## Pré-condições

- O usuário deve ter permissão para gerenciar supervisores.
- A empresa referenciada já deve existir.

## Regras específicas do fluxo

- Este fluxo usa as regras de negócio definidas em [`supervisor.md`](lpi-planning/01-entities/supervisor.md).
- Operações de cadastro e edição devem respeitar vínculo com empresa e validações opcionais de contato.
- Tentativas de exclusão devem respeitar as restrições de relacionamento com estágio.

## Pós-condições

- Os dados do supervisor são criados, atualizados, listados ou removidos de acordo com a operação solicitada.

## Comportamento esperado na UI

- A UI deve oferecer formulário de supervisor com seleção de empresa.
- Telas de listagem devem suportar paginação e filtros relevantes.
- Quando a mudança de empresa for bloqueada, a UI deve explicar a restrição de estágio ativo.

## Fora de escopo

- Reatribuição de estágio durante o gerenciamento de supervisor.
- Gerenciamento de empresa a partir da tela de supervisor.
