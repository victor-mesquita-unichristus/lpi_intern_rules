# README

## O que é este diretório

Este diretório reúne a documentação de negócio e de planejamento do sistema de gerenciamento de estágios desenvolvido no LPI.

O objetivo principal deste espaço é servir como base documental para:

- consolidar regras de domínio
- registrar decisões de modelagem
- separar entidades, fluxos e regras transversais
- sustentar geração de histórias, cards e sprints
- reduzir ambiguidades antes da implementação

Em outras palavras, este diretório funciona como fonte de verdade documental do domínio de estágios no projeto.

## Para que ele serve

Este material existe para apoiar principalmente quatro frentes:

### 1. Entendimento do domínio

Os documentos descrevem o que o sistema precisa representar e quais regras de negócio devem ser respeitadas.

### 2. Planejamento

A pasta [`lpi-planning/`](lpi-planning) organiza a documentação já consolidada em formato utilizável para planejamento, revisão e decomposição de trabalho.

### 3. Implementação com menos ambiguidade

A documentação busca deixar claro:

- quais são as entidades persistidas
- quais operações são fluxos
- quais regras são transversais ao sistema
- o que ainda está decidido
- o que continua como `PENDENTE DE DECISÃO`

### 4. Preservação histórica de decisões

O diretório também preserva contexto importante sobre a evolução do modelo, inclusive diferenças entre material mais antigo e documentação consolidada mais recente.

## Estrutura do diretório

### Documentos base do domínio

Na raiz do diretório existem documentos de referência sobre conceitos centrais do domínio, como:

- [`🏢 Empresa (Company).md`](<%F0%9F%8F%A2%20Empresa%20(Company).md>)
- [`🧑‍🎓 Aluno (Student).md`](<%F0%9F%A7%91%E2%80%8D%F0%9F%8E%93%20Aluno%20(Student).md>)
- [`👨‍🏫 Supervisor (Supervisor).md`](<%F0%9F%91%A8%E2%80%8D%F0%9F%8F%AB%20Supervisor%20(Supervisor).md>)
- [`👤 Usuário (User).md`](<%F0%9F%91%A4%20Usu%C3%A1rio%20(User).md>)
- [`📘 Curso (Course).md`](<%F0%9F%93%98%20Curso%20(Course).md>)
- [`📘 Agente Integrador (Agent Integrator).md`](<%F0%9F%93%98%20Agente%20Integrador%20(Agent%20Integrator).md>)
- [`👩‍💼 Estágio (Intern).md`](<%F0%9F%91%A9%E2%80%8D%F0%9F%92%BC%20Est%C3%A1gio%20(Intern).md>)
- [`🔗 Relacionamentos e integridade.md`](%F0%9F%94%97%20Relacionamentos%20e%20integridade.md)

Esses arquivos funcionam como material-base de regras e contexto.

### Documentação consolidada de planejamento

A pasta [`lpi-planning/`](lpi-planning) organiza o material em camadas mais operacionais:

- [`lpi-planning/01-entities/`](lpi-planning/01-entities)
  - documentação das entidades persistidas
- [`lpi-planning/02-flows/`](lpi-planning/02-flows)
  - documentação dos fluxos operacionais
- [`lpi-planning/03-cross-cutting/`](lpi-planning/03-cross-cutting)
  - regras transversais, como soft delete e autorização
- [`lpi-planning/04-templates/`](lpi-planning/04-templates)
  - templates para histórias, cards e sprints
- [`lpi-planning/05-prompts/`](lpi-planning/05-prompts)
  - prompts auxiliares para geração de artefatos
- [`lpi-planning/06-operational/`](lpi-planning/06-operational)
  - histórias, cards, sprints e alocação do time
- [`lpi-planning/00-diagnosis.md`](lpi-planning/00-diagnosis.md)
  - diagnóstico crítico de consistência da documentação

## Como este material deve ser lido

A leitura correta do diretório segue esta lógica:

1. entidades são a fonte de verdade do dado persistido
2. fluxos explicam como o sistema cria ou altera dados
3. regras transversais valem para mais de uma parte do sistema
4. artefatos operacionais traduzem a documentação em planejamento executável

## Princípios documentais deste diretório

Este diretório foi organizado para seguir alguns princípios:

- não misturar entidade com fluxo
- não inventar comportamento ausente
- explicitar conflitos e inconsistências
- marcar pontos abertos como `PENDENTE DE DECISÃO`
- preservar histórico quando decisões mais novas substituem modelos anteriores
- priorizar clareza, consistência e rastreabilidade

## Modelo atual mais importante do domínio

Um dos pontos centrais documentados aqui é o modelo de estágio baseado em vínculo e snapshots contratuais:

- [`Internship`](lpi-planning/01-entities/internship.md) representa a identidade do vínculo entre aluno e empresa
- [`InternshipTerm`](lpi-planning/01-entities/internship-term.md) representa o estado contratual em cada período
- mudanças contratuais não sobrescrevem histórico; geram novos termos

Esse modelo impacta diretamente a leitura das entidades, dos fluxos e do planejamento.

## Quando consultar este diretório

Este diretório deve ser consultado quando for necessário:

- entender uma regra de negócio antes de implementar
- revisar se uma tarefa está alinhada ao domínio atual
- gerar histórias, cards ou sprints
- validar se um fluxo está respeitando a modelagem vigente
- identificar o que ainda depende de decisão formal

## Resumo

Este diretório é o espaço de documentação estruturada do domínio de estágios do projeto LPI.

Ele serve para transformar conhecimento disperso em material claro, consistente e utilizável por produto, engenharia e planejamento.
