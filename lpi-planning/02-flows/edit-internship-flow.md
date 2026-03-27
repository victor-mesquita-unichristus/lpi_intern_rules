# Fluxo de Edição de Estágio

## Objetivo do fluxo

Atualizar dados permitidos de um estágio existente sem sobrescrever histórico contratual.

## Entidades afetadas

- `Internship`
- `InternshipTerm`

## Observação de enquadramento

Este fluxo não redefine regras de entidade.

Ele apenas operacionaliza a modelagem atual:

- dados de identidade permanecem em `Internship`
- dados contratuais vivem em `InternshipTerm`
- alterações contratuais usam snapshots

## Pré-condições

- O estágio já deve existir.
- O usuário deve ter permissão para editar estágios.

## Regras específicas do fluxo

- Este fluxo não deve sobrescrever termos já existentes.
- Se a alteração solicitada afetar condições contratuais, o sistema deve criar um novo `InternshipTerm` em vez de editar o termo atual.
- O mecanismo técnico já definido para esse caso é: criar novo snapshot, manter o mesmo `type` do termo revisado e preencher `revisedFromTermId`.
- O novo termo deve manter o mesmo `type` do termo revisado.
- O novo termo deve preencher `revisedFromTermId` para marcar a revisão do snapshot anterior.
- Mudança de empresa não é tratada como edição do estágio. Nessa situação, o estágio atual deve ser encerrado e um novo estágio deve ser criado.
- `terminationDate` não é tratado neste fluxo e continua pertencendo ao fluxo de rescisão.
- Após o preenchimento de `terminationDate`, este fluxo não pode gerar novos termos nem revisar termos existentes.
- `PENDENTE DE DECISÃO`: confirmar quais campos não contratuais de `Internship`, além de `companyId`, podem ser alterados após a criação do vínculo.
- `PENDENTE DE DECISÃO`: definir o critério operacional para decidir quando uma mudança contratual deve usar este fluxo de revisão e quando deve usar o fluxo formal de aditivo.

## Distinção importante

- O mecanismo técnico de revisão contratual já está definido.
- O critério operacional para escolher entre revisão contratual e aditivo formal ainda não está totalmente definido.
- A documentação não deve tratar essa escolha operacional como resolvida enquanto ela permanecer `PENDENTE DE DECISÃO`.

## Pós-condições

- O histórico contratual permanece preservado.
- Quando a alteração for contratual, um novo termo passa a representar o estado vigente com vínculo explícito de revisão para o termo anterior.

## Comportamento esperado na UI

- A UI deve separar claramente dados do estágio e dados do termo vigente.
- A interface não deve transmitir a ideia de edição destrutiva do termo atual.
- Ações de aditivo e rescisão devem continuar aparecendo como operações separadas.

## Fora de escopo

- Criação inicial do estágio.
- Registro de rescisão.
- Mudança de empresa dentro do mesmo estágio.
