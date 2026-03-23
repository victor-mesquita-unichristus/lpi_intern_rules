# Fluxo de Gerenciamento de Aluno

## Objetivo do fluxo

Operar cadastro, edição, listagem e exclusão de alunos em telas administrativas.

## Entidades afetadas

- Aluno
- Curso

## Campos alterados

- Campos cadastrais do aluno
- `courseId`

## Pré-condições

- O usuário deve ter permissão para gerenciar alunos.
- O curso referenciado já deve existir ao cadastrar ou editar um aluno.

## Regras específicas do fluxo

- Este fluxo usa as regras de negócio definidas em [`student.md`](lpi-planning/01-entities/student.md).
- Operações de cadastro e edição devem respeitar os requisitos de unicidade e de curso ativo já definidos na entidade.
- Tentativas de exclusão devem respeitar as restrições por vínculo com estágio.

## Pós-condições

- Os dados do aluno são criados, atualizados, listados ou removidos de acordo com a operação solicitada.

## Comportamento esperado na UI

- A UI deve oferecer formulário de aluno com seleção de curso.
- Telas de listagem devem suportar paginação e campos de busca relevantes.
- Erros de exclusão devem explicar claramente por que um aluno não pode ser removido.

## Fora de escopo

- Criação de estágio a partir da tela de aluno.
- Importação em lote ou operações massivas de aluno.
