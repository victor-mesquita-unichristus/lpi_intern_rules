# Fluxo de Rescisão

## Objetivo do fluxo

Registrar a rescisão de um estágio.

## Entidades afetadas

- Estágio

## Campos alterados

- `termination_date`
- `isActive`

## Pré-condições

- O estágio já deve existir.
- O usuário deve ter permissão para editar estágios.

## Regras específicas do fluxo

- Este fluxo altera `termination_date`.
- O fluxo usa as restrições de rescisão definidas em [`internship.md`](lpi-planning/01-entities/internship.md).
- A operação deve encerrar o estágio quando as datas armazenadas assim exigirem.
- Após a rescisão, a aplicação deve impedir operações que conflitem com o estado de estágio rescindido.
- `PENDENTE DE DECISÃO`: definir explicitamente quais operações permanecem permitidas ou bloqueadas após a rescisão.

## Pós-condições

- O estágio passa a armazenar o histórico de rescisão.
- O estágio deixa de estar ativo quando aplicável.

## Comportamento esperado na UI

- A UI deve expor apenas os campos relacionados à rescisão.
- A interface deve indicar com clareza que a operação encerra o ciclo do estágio.
- Erros de validação devem impedir datas futuras inválidas.

## Fora de escopo

- Registro de aditivo.
- Edição completa do estágio.
- Reabertura de um estágio rescindido.
