# Histórias Operacionais

Este arquivo traduz o domínio consolidado em histórias reutilizáveis sem introduzir novo escopo de produto.

## Histórias da Sprint 1

### S1-US-01 — Criar estágio pelo fluxo de TCE

Como usuário administrativo, eu quero criar um estágio pelo fluxo de TCE para que o estágio seja formalmente registrado no sistema.

**Critérios de aceite**

- O fluxo cria um registro de estágio, e não uma entidade separada de TCE.
- O usuário deve informar aluno, empresa, supervisor, carga horária, remuneração e período.
- O supervisor selecionado deve pertencer à empresa selecionada.
- O aluno selecionado não pode receber um período de estágio sobreposto.
- O estágio é criado com comportamento de status consistente com [`internship.md`](lpi-planning/01-entities/internship.md).

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
- [`lpi-planning/03-cross-cutting/authorization.md`](lpi-planning/03-cross-cutting/authorization.md)

### S1-US-02 — Guiar o preenchimento do TCE com Step Modal

Como usuário administrativo, eu quero que o fluxo de TCE seja guiado em etapas para que o preenchimento fique mais claro e menos sujeito a erros.

**Critérios de aceite**

- O front-end usa Step Modal no fluxo de TCE.
- O usuário consegue navegar entre as etapas necessárias do processo de TCE.
- O feedback de validação aparece no ponto em que o usuário informa dados inválidos.
- A seleção opcional de agente integrador fica claramente separada dos dados contratuais obrigatórios.

**Dependências**

- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)

### S1-US-03 — Exibir indicativo de estágio ativo com consistência

Como usuário, eu quero ver se um estágio está ativo para entender rapidamente sua situação atual.

**Critérios de aceite**

- A UI exibe um indicativo claro de estágio ativo.
- O status exibido é consistente com o comportamento de negócio definido em [`internship.md`](lpi-planning/01-entities/internship.md).
- Estados inconsistentes de exibição são corrigidos.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)

### S1-US-04 — Corrigir inconsistências na exibição de dados do estágio

Como usuário, eu quero que as informações do estágio sejam exibidas com consistência para que eu possa confiar no que o sistema mostra.

**Critérios de aceite**

- Inconsistências existentes na exibição de dados do estágio são corrigidas.
- Dados opcionais vazios ou ausentes são exibidos com clareza.
- Dados históricos vinculados mantêm seu significado quando renderizados em telas de detalhe.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)

## Histórias da Sprint 2

### S2-US-01 — Aplicar aditivo ao estágio

Como usuário administrativo, eu quero registrar um aditivo para um estágio para que o período de estágio possa ser estendido conforme o fluxo formal de aditivo.

**Critérios de aceite**

- O fluxo de aditivo altera apenas `amendment_start_date` e `amendment_end_date`.
- O fluxo não altera remuneração, empresa, aluno, supervisor nem outros dados-base do estágio.
- As datas de aditivo devem respeitar as regras temporais definidas em [`internship.md`](lpi-planning/01-entities/internship.md).
- O status resultante do estágio permanece consistente após o aditivo.

**Dependências**

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)

### S2-US-02 — Gerenciar agentes integradores

Como usuário administrativo, eu quero cadastrar e manter agentes integradores para que os estágios possam referenciá-los estruturalmente, em vez de texto livre.

**Critérios de aceite**

- O cadastro de agente integrador usa apenas o conjunto atual de campos do MVP.
- Nomes ativos são únicos.
- A exclusão segue a direção de soft delete por meio de `deletedAt`.
- Agentes integradores excluídos não aparecem em contextos padrão de seleção.
- O detalhe histórico do estágio continua exibindo agentes integradores já vinculados.

**Dependências**

- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)
- [`lpi-planning/03-cross-cutting/soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)

### S2-US-03 — Associar agente integrador opcional no TCE

Como usuário administrativo, eu quero selecionar opcionalmente um agente integrador durante o TCE para que o estágio reflita a participação de intermediador quando ela existir.

**Critérios de aceite**

- A associação de agente integrador é opcional no TCE.
- O fluxo armazena o relacionamento por meio de `agentIntegratorId`.
- A seleção do TCE não mostra agentes integradores inativos.
- Não é permitida entrada de agente integrador por texto livre.

**Dependências**

- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)
- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)

## Itens adiados fora do escopo definido das sprints

- A implementação do fluxo de rescisão está fora do escopo da Sprint 2.
- Exportação CSV é pós-MVP.
- Dashboards são pós-MVP.
