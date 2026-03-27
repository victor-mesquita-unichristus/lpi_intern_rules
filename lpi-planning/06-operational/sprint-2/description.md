# Sprint 2 — Refatoração Estrutural do Domínio de Estágio

## Objetivo da sprint

Consolidar a refatoração estrutural do domínio de estágio para o modelo baseado em [`Internship`](lpi-planning/01-entities/internship.md) + [`InternshipTerm`](lpi-planning/01-entities/internship-term.md), tratando o estágio como vínculo persistido e o termo como snapshot contratual por período.

O núcleo da sprint é substituir a lógica monolítica antiga por uma separação explícita entre vínculo e estado contratual, com estratégia incremental guiada por testes de domínio primeiro.

Além do núcleo do refactor, entram duas frentes adicionais já decididas:

- backend: implementação do fluxo de rescisão alinhado ao novo domínio
- frontend: prototipação e reorganização da visualização de estágio para separar vínculo e termo vigente

Nesta sprint, a entrega deve permanecer estruturalmente compatível com `ADDENDUM`, mas sem implementar o fluxo operacional de aditivo e sem recolocar `AgentIntegrator` em escopo.

## Escopo incluído

### Núcleo estrutural da sprint

- formalizar em testes de domínio as regras de [`Internship`](lpi-planning/01-entities/internship.md) e [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
- criar a persistência necessária para o modelo novo, incluindo banco, migrations e seed compatíveis
- separar vínculo e termo no domínio, removendo `Internship` como fonte monolítica das regras contratuais
- adaptar entidades, serviços, features e casos de uso impactados para o modelo de snapshots
- consolidar leitura do termo vigente e compatibilidade temporária do contrato principal achatado
- manter `placementAgency` como campo legado transitório no termo
- preservar compatibilidade estrutural com `ADDENDUM`, sem transformar aditivo em entrega operacional da sprint

### Frente adicional — backend: rescisão

- implementar o fluxo de rescisão como regra que continua válida no modelo novo
- tratar `terminationDate` como atributo de [`Internship`](lpi-planning/01-entities/internship.md)
- garantir que a rescisão encerra o estágio, bloqueia novos termos e bloqueia revisão de termos
- manter a regra de que não existe reabertura nesta fase

### Frente adicional — frontend: visualização do estágio

- adaptar contratos, tipagens e mapeamentos do frontend no recorte necessário para TCE e leitura principal
- prototipar uma nova organização visual para a tela de estágio
- separar visualmente dados do vínculo e dados do termo vigente
- preparar espaço plausível para histórico futuro, sem exibir histórico nesta sprint

## Escopo excluído

- fluxo operacional de aditivo
- histórico de termos visível na UI
- reabertura de estágio rescindido
- retorno de `AgentIntegrator` ao escopo desta implementação
- migração complexa de dados legados; reset de banco em desenvolvimento continua aceitável nesta fase
- refinamento estético final desvinculado da reorganização estrutural da tela
- CSV
- dashboards
- filtros avançados
- consolidação de soft delete em entidades fora do recorte direto desta sprint

## Abordagem metodológica

Esta sprint não começa por integração, não começa por frontend e não começa por “feature pronta”.

Ela começa por formalização das regras do novo modelo em testes.

## Ordem oficial de execução

1. `Lote 0` — testes de domínio
2. banco / migration / seed
3. entidades e domínio
4. casos de uso
5. read model e contratos
6. integração

Essa ordem existe para reduzir ambiguidade antes de mexer em persistência, serviços e integração, e para evitar que o frontend avance sobre contratos ainda instáveis.

## Blocos de trabalho

### 1. `Lote 0` — testes de domínio

- congelar invariantes de vínculo em [`Internship`](lpi-planning/01-entities/internship.md)
- congelar invariantes de snapshot em [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
- cobrir termo válido, termo vigente, revisão, rescisão e exclusão lógica
- transformar o novo modelo em especificação executável antes da implementação principal

### 2. Modelagem e persistência

- criar a estrutura persistida de [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
- ajustar o modelo persistido de [`Internship`](lpi-planning/01-entities/internship.md) para o novo recorte
- executar migrations e adaptar seed ao novo desenho

### 3. Entidades e domínio

- separar regras de vínculo das regras contratuais
- mover supervisor para o termo
- manter `placementAgency` como legado transitório
- preservar compatibilidade estrutural com `ADDENDUM`

### 4. Casos de uso

- adaptar TCE para criar vínculo + termo inicial
- reinterpretar atualização contratual do termo vigente como operação compatível com snapshots
- impedir continuidade contratual indevida após rescisão

### 5. Read model e contratos

- consolidar leitura baseada em vínculo + termo vigente
- manter compatibilidade temporária do contrato principal achatado onde necessário
- alinhar contratos consumidos pelo frontend sem recolocar o modelo monolítico como fonte de verdade

### 6. Fluxo de rescisão

- implementar rescisão definitiva em [`Internship`](lpi-planning/01-entities/internship.md)
- bloquear novos termos após rescisão
- bloquear revisão de termos após rescisão
- preservar histórico já existente

### 7. Frontend operacional

- adaptar tipagens, contratos e consumo do TCE no recorte compatível da sprint
- reorganizar a leitura do detalhe do estágio para vínculo + termo vigente
- usar prototipação funcional como apoio direto à reorganização da tela

## Critério de sucesso da sprint

A sprint é bem-sucedida quando:

- o novo modelo fica formalizado por testes de domínio antes da integração principal
- o backend persiste vínculo e termo em [`Internship`](lpi-planning/01-entities/internship.md) + [`InternshipTerm`](lpi-planning/01-entities/internship-term.md)
- o sistema deixa de depender operacionalmente do estágio monolítico antigo como fonte de verdade contratual
- TCE e leitura principal passam a operar com vínculo + termo vigente, ainda com compatibilidade temporária do contrato achatado quando necessário
- o fluxo de rescisão funciona no modelo novo, grava `terminationDate` no vínculo, encerra o estágio e impede novos termos e revisões
- o frontend possui protótipo funcional e reorganização coerente da tela, separando vínculo e termo vigente e preservando espaço para histórico futuro
- o fluxo operacional de aditivo continua fora da entrega, embora o modelo permaneça compatível com `ADDENDUM`

## Riscos principais

- iniciar implementação sem fechar primeiro a suíte de regras do `Lote 0`
- migrations e seed manterem dependências ocultas do modelo antigo
- divergência entre escrita do backend e leitura do termo vigente
- quebra de contratos entre backend e frontend durante a transição de compatibilidade
- rescisão ser implementada como remendo do modelo antigo, em vez de regra permanente do vínculo
- frontend avançar para tela final antes da estabilização mínima do read model

## Pair programming recomendado

- backend ↔ backend no início da sprint para fechar suíte do `Lote 0`, modelagem persistida e invariantes principais
- backend ↔ backend na implementação da rescisão para garantir aderência às regras do vínculo
- backend ↔ frontend no momento em que o read model e os contratos compatíveis estabilizarem
- frontend ↔ frontend durante a consolidação do protótipo e da reorganização da tela

## Nota operacional

- `Frontend B` pode começar cedo pela prototipação funcional da tela.
- A implementação operacional do detalhe depende da estabilização mínima do read model e dos contratos definidos no backend.
