# Sprint 2 — Refatoração Estrutural do Domínio de Estágio

## Objetivo da sprint

Consolidar a transição do domínio de estágio para o modelo baseado em [`Internship`](lpi-planning/01-entities/internship.md) + [`InternshipTerm`](lpi-planning/01-entities/internship-term.md), adaptando persistência, domínio, testes, seeds, contratos e telas principais para que o sistema opere com termo vigente e sem dependência operacional do modelo antigo.

## Escopo incluído

### Backend

- criar a estrutura persistida de [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
- executar migrations da nova modelagem
- ajustar ou remover a dependência dos campos contratuais antigos em [`Internship`](lpi-planning/01-entities/internship.md)
- refatorar o domínio de [`Internship`](lpi-planning/01-entities/internship.md) e [`Supervisor`](lpi-planning/01-entities/supervisor.md)
- refatorar services, features e casos de uso impactados
- implementar leitura consistente do termo vigente
- refatorar testes de entidades, services, features e integração
- adaptar seeds à nova estrutura

### Frontend

- refatorar contratos, tipagens e mapeamentos afetados
- adaptar o fluxo de TCE ao novo payload e resposta
- adaptar os fluxos que dependem da leitura operacional do estágio
- refatorar a tela de detalhe do estágio para separar dados do vínculo e dados do termo vigente
- preparar a estrutura visual para histórico futuro sem exibir histórico nesta sprint
- realizar prototipação funcional rápida para alinhar estrutura e UX da nova tela

## Escopo excluído

- histórico de termos visível na UI
- revisão de termo no frontend
- fluxo de rescisão
- Agente Integrador como feature principal desta sprint
- CSV
- dashboards
- filtros avançados
- soft delete completo em todas as entidades

## Blocos de trabalho

### 1. Modelagem e persistência

- criar [`InternshipTerm`](lpi-planning/01-entities/internship-term.md) na persistência
- executar migrations da nova estrutura
- remover dependência operacional dos campos antigos em [`Internship`](lpi-planning/01-entities/internship.md)

### 2. Refatoração de domínio

- refatorar [`Internship`](lpi-planning/01-entities/internship.md)
- refatorar [`Supervisor`](lpi-planning/01-entities/supervisor.md) conforme o novo vínculo com termo
- adaptar services, features e casos de uso impactados
- consolidar leitura do termo vigente

### 3. Testes

- atualizar testes das entidades impactadas
- atualizar testes de services e features
- atualizar testes de integração

### 4. Seeds

- adaptar seeds ao novo formato de estágio e termo

### 5. Contratos e fluxos do frontend

- refatorar contratos e tipagens
- ajustar TCE
- ajustar leitura do estágio baseada em termo vigente
- corrigir mapeamentos e estados visuais

### 6. Refatoração da tela de detalhe

- separar visualmente dados do vínculo e dados do termo vigente
- preparar a estrutura para histórico futuro sem exibi-lo agora

### 7. Prototipação funcional de apoio

- prototipar rapidamente a nova estrutura da tela de detalhe
- usar o protótipo como referência de implementação ainda nesta sprint
- limitar a atividade a alinhamento estrutural e UX, sem abrir uma trilha estética separada

## Ordem sugerida de execução

1. Modelagem e persistência
2. Refatoração de domínio
3. Contratos e fluxos do frontend
4. Prototipação funcional de apoio
5. Refatoração da tela de detalhe
6. Testes
7. Seeds

Essa ordem existe para deixar claras as dependências principais: persistência e leitura do termo vigente precisam estabilizar antes da consolidação dos contratos e da implementação final do detalhe no frontend.

## Critério de sucesso da sprint

A sprint é bem-sucedida quando:

- o backend persiste estágio e termo no modelo novo
- o sistema deixa de depender operacionalmente dos campos contratuais antigos em [`Internship`](lpi-planning/01-entities/internship.md)
- os fluxos principais de criação e leitura funcionam com base no termo vigente
- os testes impactados passam a refletir a nova modelagem
- as seeds funcionam com a nova estrutura
- o frontend consome os contratos novos, exibe separadamente vínculo e termo vigente e não tenta expor histórico de termos
- a prototipação funcional da tela é convertida em referência concreta de implementação dentro da sprint

## Riscos principais

- migrations incompletas deixarem dependências ocultas do modelo antigo
- divergência entre escrita do backend e leitura do termo vigente
- quebra de contratos entre backend e frontend durante a transição
- refatoração de testes consumir mais tempo do que o previsto
- seeds desatualizadas mascararem problemas reais da modelagem nova
- frontend implementar visual sem alinhamento suficiente com a resposta operacional do backend

## Pair programming recomendado

- backend ↔ backend no início da sprint para fechar modelagem persistida, migrations e leitura do termo vigente
- backend ↔ frontend no meio da sprint para alinhar contratos de TCE, leitura do estágio e detalhe da tela
- frontend ↔ frontend durante a refatoração visual para alinhar a separação entre vínculo e termo vigente e consolidar o protótipo funcional

## Ponto adicional para a sprint ficar redonda

- É necessário validar explicitamente todos os pontos de leitura operacional do estágio que alimentam o frontend, porque o sucesso da sprint depende menos do cadastro isolado e mais da consistência entre persistência nova, leitura do termo vigente e tela de detalhe.
- Operacionalmente, `Frontend B` pode começar cedo pela prototipação e pela estrutura visual da tela, mas a implementação final do detalhe depende da estabilização do contrato de leitura do termo vigente no backend.
