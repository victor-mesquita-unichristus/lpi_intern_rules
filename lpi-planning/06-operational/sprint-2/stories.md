# Histórias da Sprint 2

## Histórias

### S2-US-01 — Registrar aditivo criando novo termo de estágio

Como usuário administrativo, eu quero registrar um aditivo para um estágio para que as novas condições contratuais sejam armazenadas sem sobrescrever o histórico.

**Critérios de aceite**

- O fluxo de aditivo cria um novo `InternshipTerm` com `type = ADDENDUM`.
- O fluxo não altera campos contratuais diretamente em `Internship`.
- O termo anterior permanece imutável.
- O novo termo deve respeitar continuidade temporal e não pode se sobrepor aos termos já existentes.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)
- [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)

### S2-US-02 — Gerenciar agentes integradores

Como usuário administrativo, eu quero cadastrar e manter agentes integradores para que os termos de estágio possam referenciá-los estruturalmente, em vez de texto livre.

**Critérios de aceite**

- O cadastro de agente integrador usa apenas o conjunto atual de campos do MVP.
- Nomes ativos são únicos.
- A exclusão segue a direção de soft delete por meio de `deletedAt`.
- Agentes integradores excluídos não aparecem em contextos padrão de seleção.
- O detalhe histórico continua exibindo agentes integradores já vinculados a termos existentes.

**Dependências**

- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)
- [`lpi-planning/03-cross-cutting/soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)

### S2-US-03 — Associar agente integrador opcional no TCE

Como usuário administrativo, eu quero selecionar opcionalmente um agente integrador durante o TCE para que o termo inicial reflita a participação do intermediador quando ela existir.

**Critérios de aceite**

- A associação de agente integrador é opcional no TCE.
- O fluxo armazena o relacionamento por meio de `agentIntegratorId` em `InternshipTerm`.
- A seleção do TCE não mostra agentes integradores inativos.
- Não é permitida entrada de agente integrador por texto livre.

**Dependências**

- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)
- [`lpi-planning/01-entities/internship-term.md`](lpi-planning/01-entities/internship-term.md)
- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
