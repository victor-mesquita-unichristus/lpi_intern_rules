# Fluxo de Rescisão

## Objetivo do fluxo

Registrar a rescisão de um estágio.

## Entidades afetadas

- `Internship`

## Campos alterados

- `terminationDate`

## Pré-condições

- O estágio já deve existir.
- O usuário deve ter permissão para editar estágios.

## Regras específicas do fluxo

- Este fluxo altera `terminationDate` em `Internship`.
- O fluxo usa as restrições de rescisão definidas em [`internship.md`](lpi-planning/01-entities/internship.md).
- Após a rescisão, o estágio é encerrado.
- Após a rescisão, não podem ser criados novos `InternshipTerm` para esse estágio.
- Após a rescisão, não pode haver revisão de termos.
- O fluxo não edita nem remove termos históricos já registrados.
- `PENDENTE DE DECISÃO`: confirmar se existe política formal de reabertura após rescisão.

## Pós-condições

- O estágio passa a armazenar a rescisão em `terminationDate`.
- O fluxo bloqueia a criação de novos termos para o estágio rescindido.
- Os termos históricos permanecem preservados.

## Comportamento esperado na UI

- A UI deve expor apenas os campos relacionados à rescisão.
- A interface deve indicar com clareza que a operação encerra o ciclo do estágio.
- Erros de validação devem impedir datas de rescisão inválidas.

## Fora de escopo

- Registro de aditivo.
- Edição destrutiva de termos históricos.
- Reabertura de um estágio rescindido.
