# Agente Integrador

## Status na implementação atual

- `AgentIntegrator` não entra nesta implementação.
- Nesta fase, o sistema preserva `placementAgency` como campo legado `string nullable` em `InternshipTerm`.
- A separação para entidade própria fica para entrega posterior.

## Propósito futuro

Representa uma organização intermediadora que poderá participar opcionalmente das condições contratuais de um estágio por meio de `InternshipTerm`.

## Campos relevantes previstos

- `name`
- `deletedAt`

## Regras previstas de cadastro

- `name` é obrigatório e não pode ser vazio.
- `name` é normalizado com remoção de espaços extras nas extremidades.
- `name` deve ter no máximo 155 caracteres.
- Nomes ativos devem ser únicos, sem diferenciar maiúsculas de minúsculas.

## Regras previstas de edição

- O nome pode ser editado desde que a unicidade entre registros ativos seja preservada.
- A edição não deve quebrar vínculos históricos já existentes com termos de estágio.

## Regras previstas de exclusão

- A exclusão é lógica por meio de `deletedAt`.
- Referências históricas devem ser preservadas após a exclusão.

## Relacionamentos previstos

- Um agente integrador poderá estar vinculado a muitos termos de estágio.
- Um `InternshipTerm` poderá ter zero ou um `agentIntegratorId` quando essa entrega existir.

## Invariantes previstos

- Associações usarão identificador, nunca texto livre.
- Registros com `deletedAt` preenchido não poderão ser associados a novos `InternshipTerm`.
- Vínculos históricos deverão continuar visíveis quando já existentes.

## Observações

- Este documento permanece como referência de entrega futura.
- Ele não deve ser lido como escopo da implementação atual.
