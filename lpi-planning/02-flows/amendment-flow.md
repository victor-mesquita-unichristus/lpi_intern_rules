# Fluxo de Aditivo

## Objetivo do fluxo

Registrar um aditivo em um estágio existente.

No modelo atual, aditivo não altera diretamente o estágio nem sobrescreve o termo vigente.

Aditivo significa a criação de um novo `InternshipTerm` com `type = ADDENDUM`.

## Entidades afetadas

- `Internship`
- `InternshipTerm`

## Dados criados no fluxo

- novo `InternshipTerm`

## Pré-condições

- O estágio já deve existir.
- O usuário deve ter permissão para editar estágios.
- O estágio não pode estar rescindido.
- O novo termo deve respeitar a continuidade temporal do estágio.
- O supervisor informado deve pertencer à empresa do estágio.
- Se utilizado, o agente integrador deve existir e estar ativo.

## Regras específicas do fluxo

- O fluxo cria um novo `InternshipTerm` com `type = ADDENDUM`.
- O fluxo não edita o termo atual.
- O fluxo não edita campos de `Internship`.
- O fluxo deve seguir as regras definidas em [`internship.md`](lpi-planning/01-entities/internship.md) e [`internship-term.md`](lpi-planning/01-entities/internship-term.md).
- Não pode haver sobreposição entre o novo termo e termos anteriores do mesmo estágio.
- O histórico existente deve permanecer imutável.
- A empresa do estágio não muda neste fluxo.
- O aluno do estágio não muda neste fluxo.

## Pós-condições

- Um novo termo do tipo `ADDENDUM` passa a existir para o estágio.
- O histórico contratual do estágio é preservado sem sobrescrita.

## Comportamento esperado na UI

- A UI deve expor os campos contratuais do novo termo.
- Campos históricos já registrados devem ser exibidos como referência e não como edição do termo anterior.
- O usuário deve receber feedback claro de validação para continuidade temporal inválida.

## Fora de escopo

- Edição dos dados-base do estágio.
- Criação de um novo estágio.
- Registro de rescisão.
