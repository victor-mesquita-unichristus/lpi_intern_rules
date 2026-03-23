# 📘 Curso (Course)

## Regras gerais

- O curso deve ter um nome obrigatório, não vazio e com no máximo 155 caracteres.
- O sistema normaliza o nome, removendo espaços extras no início e no fim.
- O nome do curso deve ser único entre cursos ativos.
- Não podem existir dois cursos ativos com o mesmo nome, mesmo com diferença apenas de maiúsculas ou minúsculas.

## Status e ciclo de vida

- O curso pode ser criado como ativo ou inativo.
- Quando o status não é informado, ele nasce ativo.
- O curso pode ser editado, desde que continue respeitando as regras de nome e unicidade.
- O curso não pode ser editado se não existir no sistema como curso ativo.
- A exclusão é lógica: o curso não é removido, apenas marcado como inativo.
- Cursos inativos não aparecem na listagem padrão nem na busca por identificador.
- Um curso não pode ser inativado se houver estudantes vinculados a ele.

## Busca e listagem

- A listagem deve exibir somente cursos ativos, com paginação.
- A busca de cursos é feita por nome e aceita correspondência parcial.

## Relacionamento com estudante

- Todo estudante deve estar vinculado a um curso.
- Um estudante só pode ser criado ou editado com um curso existente e ativo.
- Não é permitido vincular estudante a curso inexistente ou inativo.

## Pontos de atenção

- Há divergência interna na classificação de alguns erros de curso não encontrado, embora a situação de negócio seja a mesma.
- A regra de atualização está correta, mas o contrato atual ainda pode ficar mais explícito.
