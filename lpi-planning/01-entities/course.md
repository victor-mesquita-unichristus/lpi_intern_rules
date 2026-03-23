# Curso

## Propósito

Representa o curso acadêmico ao qual um aluno pertence.

## Campos relevantes

- `name`
- `isActive` ou estado equivalente de ativo

## Regras de cadastro

- `name` é obrigatório e não pode ser vazio.
- `name` deve ter no máximo 155 caracteres.
- O sistema remove espaços extras.
- Nomes de curso ativos devem ser únicos, sem diferenciar maiúsculas de minúsculas.
- Cursos nascem ativos por padrão.

## Regras de edição

- Um curso pode ser editado desde que mantenha validade e unicidade do nome.

## Regras de exclusão

- A exclusão é lógica, usando um estado inativo.
- Um curso não pode ser inativado se houver alunos vinculados a ele.

## Relacionamentos

- Um curso possui muitos alunos.

## Invariantes

- Alunos só podem referenciar cursos existentes e ativos.
- Cursos inativos ficam fora da listagem padrão e da busca padrão.

## Observações de MVP

- Comportamentos de busca e paginação são tratados como preocupação transversal de listagem.
