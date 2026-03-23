# Fluxo de TCE

## Objetivo do fluxo

Criar um novo estágio por meio da operação de TCE.

No MVP, TCE não é uma entidade persistida separada. O fluxo cria o próprio estágio.

## Entidades afetadas

- Estágio
- Aluno
- Empresa
- Supervisor
- Agente Integrador

## Campos alterados

- `studentId`
- `companyId`
- `supervisorId`
- `agentIntegratorId`
- `isMandatory`
- `internship_payment`
- `working_hours`
- `start_date`
- `end_date`
- `meal_allowance`
- `transport_allowance`
- `isActive`

## Pré-condições

- Aluno, empresa e supervisor já devem existir.
- Se utilizado, o agente integrador já deve existir.
- O usuário deve ter permissão para criar estágios.

## Regras específicas do fluxo

- O fluxo cria um novo estágio.
- O fluxo usa as regras de domínio definidas em [`internship.md`](lpi-planning/01-entities/internship.md).
- O estágio é criado inicialmente como ativo quando as datas permitirem isso.
- O fluxo pode associar opcionalmente um `agentIntegratorId`.
- O fluxo não deve permitir entrada de agente integrador por texto livre.

## Pós-condições

- Um novo estágio passa a existir e fica vinculado aos registros selecionados.
- O status do estágio é persistido de forma consistente com as regras de domínio.

## Comportamento esperado na UI

- O front-end usa Step Modal neste fluxo.
- A UI deve guiar o usuário pela seleção de aluno, empresa, supervisor e dados contratuais.
- A seleção opcional de agente integrador deve estar claramente indicada.
- Agentes integradores inativos não devem aparecer no dropdown do TCE.

## Fora de escopo

- Operações de aditivo.
- Operações de rescisão.
- Edições estruturais em um estágio já criado fora deste fluxo de criação.
