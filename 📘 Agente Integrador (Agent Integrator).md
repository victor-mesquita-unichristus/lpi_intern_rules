# 📘 Agente Integrador (Agent Integrator)

Um agente integrador é uma entidade cadastrada no sistema que pode ser associada a um estágio para representar a participação de um intermediador no processo de estágio.

O agente integrador possui cadastro próprio no sistema e não deve ser informado por texto livre no TCE.

## Regras de cadastro

- O nome do agente integrador é obrigatório.
- O nome do agente integrador não pode ser vazio.
- O sistema remove espaços extras no início e no fim do nome.
- O nome do agente integrador não pode ultrapassar 155 caracteres.
- Cada nome de agente integrador deve ser único entre registros ativos.
- Não podem existir dois agentes integradores ativos com o mesmo nome, mesmo com diferença apenas de maiúsculas ou minúsculas.
- Um agente integrador nasce ativo por padrão.
- No MVP, o cadastro possui apenas o campo `name`.

## Regras de edição

- Um agente integrador pode ser editado.
- A edição do nome deve continuar respeitando a regra de unicidade entre registros ativos.
- A edição de um agente integrador não deve quebrar ou alterar os estágios já vinculados a ele.

## Regras de exclusão

- A exclusão de agente integrador é lógica.
- Quando um agente integrador é excluído, o sistema registra a data de exclusão no campo `deletedAt`.
- Agentes integradores com `deletedAt` preenchido são considerados inativos.
- Agentes integradores inativos não devem aparecer na listagem padrão.
- Agentes integradores inativos não devem aparecer no campo de seleção do TCE.
- Agentes integradores já associados a estágios continuam aparecendo no detalhe desses estágios, mesmo após a exclusão lógica.
- O sistema não deve remover fisicamente agentes integradores do banco de dados.

## Regras de relacionamento com estágio

- Um estágio pode ter zero ou um agente integrador associado.
- A associação entre estágio e agente integrador é opcional.
- Um agente integrador pode estar associado a vários estágios.
- O vínculo entre estágio e agente integrador deve ser feito por identificador (`agentIntegratorId`) e nunca por texto.
- O sistema não deve permitir associar um estágio a um agente integrador inexistente.
- O sistema não deve permitir associar um estágio a um agente integrador inativo.
- Se um agente integrador for excluído após ter sido associado a um estágio, o vínculo histórico deve ser preservado.

## Regras no TCE

- No formulário do TCE, o agente integrador deve ser selecionado por meio de um campo de busca.
- O campo de seleção deve listar apenas agentes integradores ativos.
- O campo de agente integrador no TCE é opcional.
- Se o agente integrador não for informado, o estágio deve ser criado normalmente.

## Regras de visualização

- No detalhe do estágio, o sistema deve exibir o nome do agente integrador associado quando existir.
- Quando um estágio não possuir agente integrador associado, o sistema deve exibir uma indicação clara de ausência de informação.
- O sistema não deve exibir valores `null`, `undefined` ou campos vazios sem contexto.

## Regras de busca e listagem

- A listagem de agentes integradores deve ser paginada.
- A busca de agentes integradores deve permitir correspondência parcial por nome.
- A listagem padrão deve exibir apenas agentes integradores ativos.
- O sistema pode permitir filtragem por status ativo ou inativo em telas administrativas.

## Estrutura de dados (MVP)

A entidade de agente integrador deve possuir, no mínimo, os seguintes campos:

- `id`
- `name`
- `createdAt`
- `updatedAt`
- `deletedAt`

O relacionamento com estágio deve ocorrer por meio do campo `agentIntegratorId` na tabela de estágios.

## Comportamento esperado do sistema

- O sistema deve impedir duplicidade de agentes integradores ativos.
- O sistema deve garantir consistência entre estágios e agentes integradores associados.
- O sistema deve preservar histórico de estágios mesmo após exclusão lógica do agente integrador.
- O sistema deve evitar entrada de dados inconsistentes ou não estruturados no cadastro de estágios.
