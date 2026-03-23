# Fluxo de Aditivo

## Objetivo do fluxo

Aplicar um aditivo em um estágio existente.

## Entidades afetadas

- Estágio

## Campos alterados

- `amendment_start_date`
- `amendment_end_date`

## Pré-condições

- O estágio já deve existir.
- O usuário deve ter permissão para editar estágios.
- O estágio ainda deve estar elegível para aditivo conforme as regras de domínio.

## Regras específicas do fluxo

- Este fluxo altera apenas as datas de aditivo.
- O fluxo não altera remuneração, empresa, supervisor, aluno nem outros campos contratuais.
- O fluxo consome as regras de coerência temporal definidas em [`internship.md`](lpi-planning/01-entities/internship.md).
- O escopo operacional atual assume um aditivo por estágio.
- `PENDENTE DE DECISÃO`: confirmar se o limite de um único aditivo é regra definitiva de produto ou apenas escopo da implementação atual.

## Pós-condições

- O estágio passa a armazenar as datas de aditivo de forma consistente.
- O status do estágio é recalculado quando necessário.

## Comportamento esperado na UI

- A UI deve expor apenas os campos relacionados a aditivo.
- Campos que não pertencem ao aditivo devem permanecer bloqueados durante esta operação.
- O usuário deve receber feedback claro de validação para datas de aditivo inválidas.

## Fora de escopo

- Edição dos dados-base do estágio.
- Criação de um novo estágio.
- Registro de rescisão.
