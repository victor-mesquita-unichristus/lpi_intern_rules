# Agente Integrador

## Propósito

Representa uma organização intermediadora que pode participar opcionalmente de um estágio.

## Campos relevantes

- `name`
- `deletedAt`

## Regras de cadastro

- `name` é obrigatório e não pode ser vazio.
- `name` é normalizado com remoção de espaços extras nas extremidades.
- `name` deve ter no máximo 155 caracteres.
- Nomes ativos devem ser únicos, sem diferenciar maiúsculas de minúsculas.

## Regras de edição

- O nome pode ser editado desde que a unicidade entre registros ativos seja preservada.
- A edição não deve quebrar vínculos históricos já existentes com estágios.

## Regras de exclusão

- A exclusão é lógica por meio de `deletedAt`.
- Referências históricas de estágio devem ser preservadas após a exclusão.

## Relacionamentos

- Um agente integrador pode estar vinculado a muitos estágios.
- Um estágio pode ter zero ou um `agentIntegratorId`.

## Invariantes

- Associações usam identificador, nunca texto livre.
- Agentes integradores inativos não podem ser associados a novos estágios.

## Observações de MVP

- No MVP, o cadastro mantém apenas `name` como campo principal de negócio.
- Agentes integradores inativos devem continuar aparecendo no detalhe do estágio quando já estiverem historicamente vinculados.
