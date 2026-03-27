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
- O critério operacional de revisão é o uso do end-point de update do termo vigente.
- O sistema não deve inferir automaticamente se a operação é revisão ou aditivo a partir do conteúdo alterado.
- Mudança de empresa não é tratada como edição do estágio. Nessa situação, o estágio atual deve ser encerrado e um novo estágio deve ser criado.
- `terminationDate` não é tratado neste fluxo e continua pertencendo ao fluxo de rescisão.
- Após o preenchimento de `terminationDate`, este fluxo não pode gerar novos termos nem revisar termos existentes.
- `studentId` não pode ser alterado após a criação do vínculo.
- `companyId` não pode ser alterado após a criação do vínculo.
- Nesta fase, a compatibilidade do contrato principal pode permanecer achatada para criação e leitura principal, desde que o backend preserve internamente a separação entre vínculo e termo.

## Distinção importante

- O mecanismo técnico de revisão contratual já está definido.
- O critério operacional para escolher entre revisão contratual e aditivo formal é o fluxo/end-point de origem.
- End-point de update do termo vigente gera revisão.
- End-point de aditivo gera `ADDENDUM`.

## Pós-condições

- O histórico contratual permanece preservado.
- Quando a alteração for contratual, um novo termo passa a representar o estado vigente com vínculo explícito de revisão para o termo anterior.

## Comportamento esperado na UI

- A UI deve separar claramente dados do estágio e dados do termo vigente.
- A interface não deve transmitir a ideia de edição destrutiva do termo atual.
- Ações de aditivo e rescisão devem continuar aparecendo como operações separadas.
- O contrato principal pode permanecer achatado para leitura principal, desde que a UI não trate essa compatibilidade como identidade estrutural do domínio.

## Fora de escopo

- Criação inicial do estágio.
- Registro de rescisão.
- Mudança de empresa dentro do mesmo estágio.
