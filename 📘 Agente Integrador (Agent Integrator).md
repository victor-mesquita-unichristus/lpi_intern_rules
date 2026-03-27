# 📘 Agente Integrador (Agent Integrator)

## Status na implementação atual

- `AgentIntegrator` não entra nesta implementação.
- Nesta fase, o sistema preserva `placementAgency` como campo legado `string nullable` em `InternshipTerm`.
- A separação para entidade própria fica para entrega posterior.

## Propósito futuro

Representa uma organização intermediadora que poderá participar opcionalmente das condições contratuais de um estágio por meio de `InternshipTerm`.

## Regras previstas de cadastro

- `name` é obrigatório e não pode ser vazio.
- O sistema remove espaços extras no início e no fim do nome.
- `name` deve ter no máximo 155 caracteres.
- Cada nome ativo deve ser único entre registros não removidos logicamente.

## Regras previstas de edição

- O nome pode ser editado desde que a unicidade entre registros ativos seja preservada.
- A edição não deve quebrar vínculos históricos já existentes.

## Regras previstas de exclusão

- A exclusão é lógica por meio de `deletedAt`.
- Referências históricas devem ser preservadas após a exclusão.

## Regras previstas de relacionamento

- Um agente integrador poderá estar vinculado a muitos termos de estágio.
- Um `InternshipTerm` poderá ter zero ou um `agentIntegratorId` quando essa entrega existir.
- O vínculo deverá usar identificador, nunca texto livre.

## Estrutura de dados prevista

- `id`
- `name`
- `createdAt`
- `updatedAt`
- `deletedAt`

## Observação

- Este documento permanece como referência de entrega futura.
- Ele não deve ser lido como escopo da implementação atual.
