# Fluxo de TCE

## Objetivo do fluxo

Criar um novo estágio por meio da operação de TCE.

TCE não é uma entidade persistida separada.

No modelo atual, TCE significa a criação combinada de:

- um `Internship`
- um `InternshipTerm` com `type = INITIAL`

## Entidades afetadas

- `Internship`
- `InternshipTerm`
- Aluno
- Empresa
- Supervisor
- Agente Integrador

## Dados criados no fluxo

### Em `Internship`

- `studentId`
- `companyId`
- `terminationDate = null`

### Em `InternshipTerm`

- `type = INITIAL`
- `startDate`
- `endDate`
- `supervisorId`
- `internshipPayment`
- `workingHours`
- `mealAllowance`
- `transportAllowance`
- `isMandatory`
- `agentIntegratorId`

## Pré-condições

- Aluno, empresa e supervisor já devem existir.
- O supervisor deve pertencer à empresa selecionada para o estágio.
- Se utilizado, o agente integrador já deve existir e estar ativo.
- O usuário deve ter permissão para criar estágios.

## Regras específicas do fluxo

- O fluxo cria um novo `Internship`.
- O fluxo cria um novo `InternshipTerm` inicial vinculado ao estágio criado.
- O fluxo usa as regras de domínio definidas em [`internship.md`](lpi-planning/01-entities/internship.md) e [`internship-term.md`](lpi-planning/01-entities/internship-term.md).
- O fluxo não deve persistir TCE como entidade separada.
- O fluxo não deve permitir entrada de agente integrador por texto livre.
- Quaisquer mudanças futuras nas condições contratuais não devem editar esse termo inicial; devem gerar novo termo conforme o modelo de snapshot.

## Pós-condições

- Um novo estágio passa a existir e fica vinculado ao aluno e à empresa selecionados.
- Um termo inicial passa a existir com as condições contratuais informadas no TCE.

## Comportamento esperado na UI

- O front-end usa Step Modal neste fluxo.
- A UI deve guiar o usuário pela seleção de aluno, empresa, supervisor e dados contratuais do termo inicial.
- A seleção opcional de agente integrador deve estar claramente indicada.
- Agentes integradores inativos não devem aparecer no dropdown do TCE.

## Fora de escopo

- Operações de aditivo.
- Operações de rescisão.
- Edição de termos já existentes.
