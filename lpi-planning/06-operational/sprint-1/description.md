# Sprint 1

## Contexto

Esta sprint é preservada conforme o escopo original definido à época.

- Ela antecede a introdução de [`InternshipTerm`](lpi-planning/01-entities/internship-term.md) como modelagem oficial.
- O conteúdo desta pasta não deve ser reinterpretado retroativamente pelo modelo posterior.

## Observação posterior de escopo

- As decisões finais posteriores mantêm esta sprint como registro histórico.
- Na implementação atual, `AgentIntegrator` ficou fora de escopo e `placementAgency` permanece como legado transitório.
- O fluxo de aditivo também ficou fora do escopo da sprint atual de implementação, permanecendo apenas como preparação estrutural futura.

## Objetivo

Fechar o fluxo de TCE de forma robusta, validando regras e melhorando a UX com Step Modal.

## Histórias incluídas

- `S1-US-01` — Criar estágio pelo fluxo de TCE
- `S1-US-02` — Guiar o preenchimento do TCE com Step Modal
- `S1-US-03` — Exibir indicativo de estágio ativo com consistência
- `S1-US-04` — Corrigir inconsistências na exibição de dados do estágio

## Ordem sugerida de execução

1. Consolidação de validações de TCE no backend
2. Refinamento do contrato de payload/resposta do TCE no backend
3. Estrutura do Step Modal no frontend
4. Integração do frontend com o fluxo de criação no backend
5. Indicador de ativo e correções de renderização

## Riscos

- O comportamento de validação pode expor inconsistências escondidas no tratamento antigo de estágio.
- O custo de interação no frontend pode superar a estimativa inicial.
