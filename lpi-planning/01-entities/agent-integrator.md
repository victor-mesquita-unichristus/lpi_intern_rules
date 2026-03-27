# Agente Integrador

## Propósito

Representa uma organização intermediadora que pode participar opcionalmente das condições contratuais de um estágio por meio de `InternshipTerm`.

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
- A edição não deve quebrar vínculos históricos já existentes com termos de estágio.

## Regras de exclusão

- A exclusão é lógica por meio de `deletedAt`.
- Referências históricas devem ser preservadas após a exclusão.

## Relacionamentos

- Um agente integrador pode estar vinculado a muitos termos de estágio.
- Um `InternshipTerm` pode ter zero ou um `agentIntegratorId`.

## Invariantes

- Associações usam identificador, nunca texto livre.
- Registros com `deletedAt` preenchido não podem ser associados a novos `InternshipTerm`.
- Vínculos históricos devem continuar visíveis quando já existentes.

## Observações de MVP

- No MVP, o cadastro mantém apenas `name` como campo principal de negócio.
- A entidade continua compatível com a direção global de soft delete.
