# Alocação do Time — Sprint 2

## Distribuição sugerida

### Backend A

- `S2-C01` — Criar persistência de `InternshipTerm` e migrations
- `S2-C02` — Refatorar domínio de estágio e leitura do termo vigente

### Backend B

- `S2-C03` — Refatorar casos de uso e contratos de TCE e aditivo no backend
- `S2-C04` — Refatorar testes da nova modelagem no backend
- `S2-C05` — Adaptar seeds para a nova estrutura de estágio

### Responsabilidade compartilhada em testes

- `S2-C04` tem ownership principal de `Backend B`, mas a refatoração de testes deve ser tratada como responsabilidade compartilhada entre `Backend A` e `Backend B` para evitar desequilíbrio e garantir cobertura coerente da nova modelagem.

### Frontend A

- `S2-C06` — Refatorar tipagens e contratos do frontend
- `S2-C07` — Adaptar TCE no frontend para o novo payload e resposta

### Frontend B

- `S2-C08` — Ajustar detalhe do estágio para exibir apenas o termo vigente
- `S2-C09` — Prototipar estrutura funcional da nova tela de detalhe

### Nota operacional

- `Frontend B` pode iniciar cedo pela prototipação e pela estrutura visual da nova tela.
- A implementação final do detalhe depende da estabilização do contrato de leitura do termo vigente no backend.

## Justificativa da distribuição

- Backend A concentra a base estrutural da persistência e da leitura do termo vigente, porque essa combinação define o núcleo técnico da transição.
- Backend B concentra casos de uso, testes e seeds, equilibrando a carga de backend e reduzindo gargalo em apenas uma pessoa.
- Frontend A concentra contratos e TCE, porque essas duas frentes dependem diretamente da transição do payload e da resposta do backend.
- Frontend B concentra detalhe de estágio e prototipação funcional, garantindo carga suficiente e útil no frontend sem introduzir histórico visível.

## Pair programming recomendado

- Backend A ↔ Backend B no início da sprint para fechar modelagem persistida, migrations e leitura do termo vigente.
- Backend B ↔ Frontend A no meio da sprint para alinhar contratos de TCE e resposta do estágio.
- Backend A ↔ Frontend B no meio da sprint para validar a leitura do termo vigente usada no detalhe.
- Frontend A ↔ Frontend B durante a refatoração da tela para alinhar a separação entre vínculo e termo vigente e consolidar o protótipo funcional.

## Princípios de alocação

- Manter uma responsabilidade principal por bloco de trabalho.
- Evitar paralelizar dependências críticas antes da definição mínima da persistência nova.
- Priorizar integração progressiva entre persistência, domínio e contratos.
- Tratar leitura do termo vigente como ponto de convergência obrigatório entre backend e frontend.
