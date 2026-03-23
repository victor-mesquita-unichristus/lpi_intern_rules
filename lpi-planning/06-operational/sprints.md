# Decomposição de Sprints

## Modelo de entrega

- Cadência das sprints: quinzenal
- Time: 2 estagiários de frontend + 2 estagiários de backend
- Princípio: estrutura leve, escopo fechado de sprint, entrega útil e execução orientada a aprendizado

## Sprint 1 — Escopo fechado já definido

### Objetivo

Fechar o fluxo de TCE de forma robusta, validando regras e melhorando a UX com Step Modal.

### Histórias incluídas

- `S1-US-01` — Criar estágio pelo fluxo de TCE
- `S1-US-02` — Guiar o preenchimento do TCE com Step Modal
- `S1-US-03` — Exibir indicativo de estágio ativo com consistência
- `S1-US-04` — Corrigir inconsistências na exibição de dados do estágio

### Ordem sugerida de execução

1. Consolidação de validações de TCE no backend
2. Refinamento do contrato de payload/resposta do TCE no backend
3. Estrutura do Step Modal no frontend
4. Integração do frontend com o fluxo de criação no backend
5. Indicador de ativo e correções de renderização

### Riscos

- O custo de interação no frontend pode superar a estimativa inicial
- O comportamento de validação pode expor inconsistências escondidas no tratamento antigo de estágio

## Sprint 2 — Escopo fechado já definido

### Objetivo

Expandir o fluxo de estágio com Aditivo e estruturar Agentes Integradores.

### Histórias incluídas

- `S2-US-01` — Aplicar aditivo ao estágio
- `S2-US-02` — Gerenciar agentes integradores
- `S2-US-03` — Associar agente integrador opcional no TCE

### Itens explicitamente excluídos

- Fluxo de rescisão
- Exportação CSV
- Dashboards

### Ordem sugerida de execução

1. Operação de aditivo no backend
2. Persistência e regras de seleção de agente integrador no backend
3. Fluxo de aditivo no frontend
4. Gerenciamento de agente integrador no frontend
5. Integração do TCE com seleção opcional de agente integrador

### Riscos

- A consolidação de soft delete pode expor inconsistência legada
- A integração do TCE pode ser bloqueada se o comportamento de listagem de agente integrador não estiver estabilizado antes

## Depois da Sprint 2

### Próxima trilha recomendada

- Fluxo de rescisão
- Consolidação da edição genérica de estágio
- Consolidação do modelo de soft delete nas entidades restantes

### Itens que não devem ser puxados cedo

- Exportação CSV
- Dashboards

Esses itens já são tratados como pós-MVP.
