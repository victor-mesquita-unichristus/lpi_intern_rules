# Fluxo de Edição de Estágio

## Objetivo do fluxo

Atualizar os dados cadastrais editáveis de um estágio existente.

## Entidades afetadas

- Estágio

## Campos alterados

- Campos contratuais permitidos, exceto campos de aditivo e rescisão

## Pré-condições

- O estágio já deve existir.
- O usuário deve ter permissão para editar estágios.

## Regras específicas do fluxo

- Este fluxo altera apenas os campos permitidos do estágio.
- O fluxo não trata dados de aditivo.
- O fluxo não trata dados de rescisão.
- Se o estágio já tiver iniciado, a aplicação deve respeitar as regras de imutabilidade definidas em [`internship.md`](lpi-planning/01-entities/internship.md).

## Pós-condições

- Os dados do estágio são atualizados sem quebrar invariantes de domínio.
- O status é recalculado se algum dos campos editados impactar esse comportamento.

## Comportamento esperado na UI

- A UI deve expor apenas os campos editáveis.
- Campos bloqueados devem aparecer visualmente desabilitados quando o estágio já tiver iniciado.
- Ações de aditivo e rescisão devem aparecer como operações separadas.

## Fora de escopo

- Criação de estágio.
- Registro de aditivo.
- Registro de rescisão.
