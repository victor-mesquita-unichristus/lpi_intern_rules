# Sprint 2

## Objetivo

Expandir o fluxo de estágio com aditivo baseado em novo termo e estruturar agentes integradores no modelo atualizado.

## Histórias incluídas

- `S2-US-01` — Registrar aditivo criando novo termo de estágio
- `S2-US-02` — Gerenciar agentes integradores
- `S2-US-03` — Associar agente integrador opcional no TCE

## Itens explicitamente excluídos

- Fluxo de rescisão
- Edição contratual genérica por snapshot fora do caso formal de aditivo
- Exportação CSV
- Dashboards

## Ordem sugerida de execução

1. Operação de aditivo no backend
2. Persistência e regras de seleção de agente integrador no backend
3. Fluxo de aditivo no frontend
4. Gerenciamento de agente integrador no frontend
5. Integração do TCE com seleção opcional de agente integrador

## Riscos

- A consolidação de soft delete pode expor inconsistência legada.
- A integração do TCE pode ser bloqueada se o comportamento de listagem de agente integrador não estiver estabilizado antes.
