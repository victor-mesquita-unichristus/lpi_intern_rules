# Diagnóstico do Planejamento LPI

## Escopo deste diagnóstico

Este diagnóstico revisa a estrutura atual de planejamento em [`lpi-planning/`](lpi-planning), com prioridade para:

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
- [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
- [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)
- [`lpi-planning/02-flows/termination-flow.md`](lpi-planning/02-flows/termination-flow.md)
- [`lpi-planning/03-cross-cutting/soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)
- [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)

O objetivo não é criar novo comportamento de produto, mas identificar o que já está consolidado, o que está inconsistente e o que ainda depende de decisão.

## Arquivos que já estão em boa direção

### Bons ou majoritariamente bons

- [`lpi-planning/01-entities/company.md`](lpi-planning/01-entities/company.md)
  - Está corretamente posicionado como verdade da entidade.
  - Está majoritariamente consistente com o material-base atual.

- [`lpi-planning/01-entities/supervisor.md`](lpi-planning/01-entities/supervisor.md)
  - Está corretamente focado em regras persistentes de negócio.
  - O relacionamento com empresa está documentado na camada correta.

- [`lpi-planning/01-entities/student.md`](lpi-planning/01-entities/student.md)
  - Está focado em entidade e é útil operacionalmente.
  - Precisa apenas de cuidado pontual com a regra de sobreposição, pois ela é efetivamente garantida pelo comportamento de estágio.

- [`lpi-planning/02-flows/edit-internship-flow.md`](lpi-planning/02-flows/edit-internship-flow.md)
  - Já está separado de aditivo e rescisão.
  - A direção está correta.

## Arquivos com inconsistência ou consolidação fraca

### [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)

Status: parcialmente correto, mas ainda precisa de consolidação.

Problemas encontrados:

- Coloca corretamente `Estágio` no centro do sistema.
- Já separa aditivo e rescisão como fluxos, o que está alinhado.
- Introduz `deletedAt` como se já estivesse consolidado para estágio, mas a base histórica atual explicita apenas restrições de exclusão, enquanto a nova direção diz que soft delete deve ser global sempre que possível.
- Por causa disso, o modelo de soft delete para estágio ainda não está totalmente consolidado e precisa ser documentado com cuidado para não transformar uma direção desejada em verdade atual falsa.
- A coerência temporal está resumida demais. O material-fonte antigo traz regras mais concretas de ordenação temporal que devem permanecer como verdade da entidade.
- `isActive` aparece como estado derivado, o que é consistente com o conjunto antigo de regras, mas a redação final precisa evitar inferir detalhes de implementação ainda não confirmados além do comportamento de negócio.

Conclusão:

- Boa base.
- Precisa consolidar melhor as regras temporais.
- Precisa distinguir explicitamente verdade atual de direção de soft delete.

### [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)

Status: correto na direção, mas genérico demais.

Problemas encontrados:

- Trata corretamente o TCE como criação de `Estágio`.
- Já evita redefinir a maior parte das regras de domínio.
- Ainda não conecta explicitamente o TCE à decisão de produto de que o próprio estágio é a formalização do TCE no MVP.
- Diz que o front-end pode implementar Step Modal, mas a Sprint 1 já estabelece essa direção de forma mais forte.
- Ainda falta explicitar que TCE não é uma entidade persistida separada.

Conclusão:

- Camada correta.
- Precisa de enquadramento operacional mais preciso, não de novas regras.

### [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)

Status: majoritariamente correto, mas com um ponto assertivo demais.

Problemas encontrados:

- Afirma corretamente que aditivo é um fluxo dedicado sobre `Estágio`.
- Limita corretamente os campos alterados a `amendment_start_date` e `amendment_end_date`.
- Afirma atualmente que apenas um aditivo deve ser considerado no escopo do MVP.
- Essa afirmação é compatível com a instrução mais recente, mas precisa ser escrita como escopo operacional, não como regra de domínio da entidade, salvo decisão explícita em definitivo.

Conclusão:

- Muito próximo do alvo.
- Precisa de ajuste de redação para permanecer na camada de fluxo.

### [`lpi-planning/02-flows/termination-flow.md`](lpi-planning/02-flows/termination-flow.md)

Status: majoritariamente correto, mas ainda um pouco orientado à implementação.

Problemas encontrados:

- Trata corretamente a rescisão como fluxo dedicado.
- Limita corretamente o campo alterado a `termination_date`, com efeito sistêmico sobre atividade.
- A afirmação de que operações incompatíveis posteriores devem ser bloqueadas está correta na direção, mas ainda é ampla demais.
- Sem enumeração explícita dessas operações bloqueadas, isso deve permanecer como nota controlada, não como nova regra escondida.

Conclusão:

- Boa estrutura.
- Precisa de redação um pouco mais segura.

### [`lpi-planning/03-cross-cutting/soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)

Status: inconsistente com a direção estratégica atual.

Problemas encontrados:

- Atualmente diz que soft delete se aplica a curso, agente integrador e futuras entidades administrativas.
- A direção mais recente diz que a direção do sistema é soft delete global com `deletedAt` sempre que possível.
- Portanto, o arquivo atual está estreito demais e ainda reflete uma visão local mais antiga.
- Também mistura verdade atual com preferência futura sem distingui-las explicitamente.

Conclusão:

- Precisa ser consolidado.
- Deve virar a regra transversal canônica para a direção de soft delete e para exceções conhecidas ou confirmações pendentes.

### [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)

Status: bom, mas incompleto em relação às decisões consolidadas mais recentes do produto.

Problemas encontrados:

- Já cobre `name`, `deletedAt`, unicidade, relação opcional com estágio e preservação de histórico.
- Ainda não explicita que agentes integradores inativos não devem aparecer no dropdown do TCE, o que é uma regra de produto confirmada.
- Esse comportamento toca tanto entidade quanto fluxo: a verdade da entidade é que registros inativos não podem ser associados em novas operações; a verdade do fluxo TCE é que o dropdown não deve oferecê-los.

Conclusão:

- Boa base.
- Precisa de separação mais clara entre verdade da entidade e uso operacional no TCE.

## Arquivos que ainda misturam preocupações

### Mistura leve entre entidade e fluxo

- [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
  - Menciona aditivo e rescisão como fluxos dedicados, o que é um contexto útil.
  - Precisa de cuidado para não começar a descrever comportamento operacional além da verdade da entidade.

- [`lpi-planning/01-entities/student.md`](lpi-planning/01-entities/student.md)
  - A regra de sobreposição é, no fim, uma invariante de estágio. Mantê-la aqui é aceitável como consequência relacional, mas a fonte canônica deve permanecer em [`internship.md`](lpi-planning/01-entities/internship.md).

## Regras do material antigo que conflitam com decisões recentes

### Modelo de soft delete

- Material antigo:
  - Curso usa estado inativo.
  - Agente Integrador usa `deletedAt`.
  - Estágio tinha exclusão descrita por permissões e restrições de data, não claramente como soft delete.
- Nova direção consolidada:
  - Soft delete deve ser global com `deletedAt` sempre que possível.

Status:

- Existe conflito.
- Precisa de consolidação com nota explícita quando algo ainda for apenas direção e não verdade plenamente confirmada no material anterior.

### Nomeação do TCE

- Tendência antiga:
  - TCE pode ser interpretado como artefato de termo separado.
- Nova decisão consolidada:
  - O próprio `Estágio` é a formalização persistida do TCE no MVP.

Status:

- Precisa ficar explícito em [`tce-flow.md`](lpi-planning/02-flows/tce-flow.md) e ser respeitado em [`internship.md`](lpi-planning/01-entities/internship.md).

### Aditivo e rescisão versus edição genérica

- O material antigo já trazia campos separados de aditivo e rescisão em estágio.
- A nova decisão reforça que aditivo e rescisão são fluxos dedicados, não edição genérica.

Status:

- Não há conflito real.
- Precisa apenas de redação operacional mais limpa.

## Pendências de decisão identificadas

Os pontos abaixo não devem ser inventados e devem ser marcados explicitamente quando necessário:

- `PENDENTE DE DECISÃO`: se `Estágio` já segue oficialmente `deletedAt` hoje ou se isso ainda é apenas a direção pretendida de consolidação.
- `PENDENTE DE DECISÃO`: se `Empresa`, `Aluno`, `Supervisor` e `Usuário` também estão migrando para `deletedAt`, ou se alguns ainda permanecem com restrições de hard delete no MVP.
- `PENDENTE DE DECISÃO`: se a edição de estágio pode alterar supervisor e empresa hoje, já que o contexto do produto diz “talvez supervisor, talvez empresa”, enquanto as regras antigas restringem alterações após início e não confirmam totalmente os cenários permitidos antes do início.
- `PENDENTE DE DECISÃO`: se o limite de um aditivo por estágio é escopo definitivo do produto ou apenas escopo da implementação atual.

## Ordem recomendada de saneamento

1. Consolidar [`lpi-planning/01-entities/internship.md`](lpi-planning/01-entities/internship.md)
2. Refinar [`lpi-planning/02-flows/tce-flow.md`](lpi-planning/02-flows/tce-flow.md)
3. Refinar [`lpi-planning/02-flows/amendment-flow.md`](lpi-planning/02-flows/amendment-flow.md)
4. Refinar [`lpi-planning/02-flows/termination-flow.md`](lpi-planning/02-flows/termination-flow.md)
5. Consolidar [`lpi-planning/03-cross-cutting/soft-delete.md`](lpi-planning/03-cross-cutting/soft-delete.md)
6. Refinar [`lpi-planning/01-entities/agent-integrator.md`](lpi-planning/01-entities/agent-integrator.md)

## Resumo do diagnóstico

- O repositório já tem uma direção válida em três camadas.
- O principal problema restante não é falta de estrutura, mas consolidação dos limites de verdade.
- A maior inconsistência é o modelo de soft delete.
- O alvo de saneamento com maior valor é [`internship.md`](lpi-planning/01-entities/internship.md), porque ele ancora todo o produto.
- Os arquivos de fluxo já estão próximos do formato certo e precisam mais de precisão de redação do que de redesign.
