# Alocação do Time — Sprint 2

## Distribuição sugerida

### Backend A

- `S2-C01` — `Lote 0`: formalizar o novo domínio em testes de domínio
- `S2-C02` — Modelar banco, migrations e seed do novo modelo
- `S2-C03` — Implementar entidades e regras de domínio de `Internship` + `InternshipTerm`
- `S2-C05` — Implementar read model e compatibilidade temporária do contrato achatado

### Backend B

- `S2-C04` — Adaptar casos de uso de TCE e evolução contratual ao modelo de snapshots
- `S2-C06` — Implementar fluxo de rescisão no backend
- `S2-C07` — Validar integração e regressão do backend no novo modelo

### Responsabilidade compartilhada no núcleo do backend

- `S2-C01` tem ownership principal de `Backend A`, mas deve ser executado com participação ativa de `Backend B`, porque define as regras que impactam todos os lotes seguintes.
- `S2-C06` tem ownership principal de `Backend B`, mas precisa de validação conjunta com `Backend A`, porque a rescisão afeta invariantes do vínculo, do read model e dos bloqueios pós-rescisão.

### Frontend A

- `S2-C08` — Adaptar contratos, tipagens e TCE do frontend ao recorte compatível da sprint

### Frontend B

- `S2-C09` — Prototipar a nova organização visual da tela de estágio
- `S2-C10` — Reorganizar a visualização operacional do estágio com base no protótipo

### Apoio pontual entre frentes de frontend

- `Frontend A` apoia `S2-C10` no momento em que o contrato compatível e a leitura principal estabilizarem.
- `Frontend B` pode iniciar cedo por `S2-C09`, mesmo antes da conclusão do backend estrutural.

### Nota operacional

- O backend carrega a parte mais pesada da sprint, porque a refatoração estrutural depende da ordem `testes → persistência → domínio → casos de uso → read model → integração`.
- A frente de rescisão não é paralela ao refactor como exceção isolada; ela deve ser implementada já aderente ao modelo novo.
- A implementação final da visualização do estágio depende da estabilização mínima do read model e do contrato compatível do backend.

## Justificativa da distribuição

- Backend A concentra a base estrutural da sprint, porque `Lote 0`, persistência, entidades e read model definem a espinha dorsal do refactor.
- Backend B concentra casos de uso, rescisão e integração, formando a trilha operacional que valida o modelo novo em fluxo real.
- A separação explícita da rescisão em `Backend B` reduz risco de ela virar remendo do modelo antigo e mantém ownership claro dessa frente adicional.
- Frontend A concentra contratos, tipagens e TCE, porque essa frente depende diretamente da compatibilidade temporária definida no backend.
- Frontend B concentra prototipação e reorganização da tela, garantindo avanço útil no frontend sem antecipar histórico de termos nem fluxo operacional de aditivo.

## Pair programming recomendado

- Backend A ↔ Backend B no início da sprint para fechar `S2-C01`, `S2-C02` e `S2-C03`.
- Backend A ↔ Backend B na implementação de `S2-C06` para validar bloqueios pós-rescisão e impacto no read model.
- Backend A ↔ Frontend A quando `S2-C05` estabilizar, para alinhar contrato compatível e TCE.
- Backend B ↔ Frontend B para alinhar como o estado de estágio encerrado por rescisão aparece na visualização reorganizada.
- Frontend A ↔ Frontend B após `S2-C09`, para transformar o protótipo em referência direta de `S2-C10`.

## Princípios de alocação

- Manter uma responsabilidade principal por bloco de trabalho.
- Respeitar a ordem da sprint: testes de domínio antes de persistência, persistência antes de integração.
- Evitar paralelizar implementação final de frontend antes da estabilização mínima do read model.
- Priorizar integração progressiva entre persistência, domínio, rescisão e contratos.
- Tratar leitura do termo vigente como ponto de convergência obrigatório entre backend e frontend.
