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
- `placementAgency` (`nullable`, legado)

## Pré-condições

- Aluno, empresa e supervisor já devem existir.
- O supervisor deve pertencer à empresa selecionada para o estágio.
- O usuário deve ter permissão para criar estágios.

## Regras específicas do fluxo

- O fluxo cria um novo `Internship`.
- O fluxo cria um novo `InternshipTerm` inicial vinculado ao estágio criado.
- O fluxo usa as regras de domínio definidas em [`internship.md`](lpi-planning/01-entities/internship.md) e [`internship-term.md`](lpi-planning/01-entities/internship-term.md).
- O fluxo não deve persistir TCE como entidade separada.
- Nesta fase, `placementAgency` pode ser informado como campo legado `string nullable` no termo.
- `AgentIntegrator` não faz parte desta implementação.
- Quaisquer mudanças futuras nas condições contratuais não devem editar esse termo inicial; devem gerar novo termo conforme o modelo de snapshot.

## Pós-condições

- Um novo estágio passa a existir e fica vinculado ao aluno e à empresa selecionados.
- Um termo inicial passa a existir com as condições contratuais informadas no TCE.

## Comportamento esperado na UI

- O front-end usa Step Modal neste fluxo.
- A UI deve guiar o usuário pela seleção de aluno, empresa, supervisor e dados contratuais do termo inicial.
- Nesta fase, o contrato principal pode permanecer achatado para criação e leitura principal, desde que o backend preserve internamente a separação entre vínculo e termo.
- O histórico de termos pode ser exposto por endpoint adicional específico.

## Fora de escopo

- Operações de aditivo.
- Operações de rescisão.
- Edição de termos já existentes.
