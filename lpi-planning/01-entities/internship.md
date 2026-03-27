# Estágio

## Propósito

`Internship` continua sendo a entidade central do sistema LPI.

Ela representa:

- o vínculo entre aluno e empresa
- a identidade persistida do estágio
- o ciclo de vida do estágio, incluindo rescisão e exclusão lógica

## Princípio central

- `Internship` representa a identidade do vínculo.
- `InternshipTerm` representa as condições contratuais por período.
- `Internship` não armazena dados contratuais variáveis.

## Papel no domínio

- `Internship` é a entidade âncora do domínio de estágios.
- É nela que o sistema reconhece a existência contínua do vínculo entre aluno e empresa.
- Os termos contratuais podem mudar ao longo do tempo, mas continuam pertencendo ao mesmo `Internship` enquanto o vínculo permanecer o mesmo.
- A separação entre vínculo e condições contratuais é estrutural, não apenas organizacional.
- `Internship` concentra a identidade persistida que amarra aluno, empresa, termos válidos, rescisão e exclusão lógica dentro do mesmo ciclo de vida.

## Campos

- `id`
- `studentId`
- `companyId`
- `terminationDate` (`nullable`)
- `createdAt`
- `updatedAt`
- `deletedAt` (`nullable`)

## Regras

- A empresa permanece fixa no estágio.
- `studentId` não pode ser alterado após a criação do estágio.
- Conceitualmente não existe transferência de estágio de um aluno para outro.
- Se houver necessidade de mudar a empresa, o estágio atual deve ser encerrado e um novo estágio deve ser criado.
- `Internship` não contém supervisor, `placementAgency`, datas contratuais, remuneração, carga horária nem campos de aditivo.
- `terminationDate`, quando preenchido, representa a rescisão do estágio.
- Nesta fase, a rescisão é definitiva.
- Após a rescisão, o estágio é encerrado e não pode receber novos termos.
- Após a rescisão, o estágio não pode receber revisão de termos.
- A exclusão do estágio é lógica por meio de `deletedAt`.
- A linha temporal contratual do estágio é formada pelo conjunto de termos válidos vinculados a ele.
- A coerência temporal do estágio depende da ausência de sobreposição entre termos válidos do mesmo vínculo.
- Um aluno não pode manter períodos de estágio sobrepostos, mesmo quando esses períodos pertençam a estágios diferentes.

## Ciclo de vida

- O estágio nasce como identidade persistida do vínculo entre aluno e empresa.
- O TCE cria o estágio junto com o termo inicial.
- A evolução contratual ocorre por novos registros em `InternshipTerm`.
- A rescisão encerra o ciclo de vida do estágio sem apagar seu histórico.
- Depois da rescisão, o estágio preserva histórico, mas não admite novos termos nem revisão de termos existentes.
- A exclusão lógica remove o estágio das listagens padrão sem apagar seu histórico persistido.

## Relacionamentos

- Um estágio pertence a um aluno.
- Um estágio pertence a uma empresa.
- Um estágio deve possuir ao menos um registro em `InternshipTerm`, criado no TCE como termo inicial.
- Um estágio pode possuir termos adicionais ao longo do tempo, desde que respeitem a continuidade temporal e o estado do estágio.

## Invariantes

- `Internship` é a fonte da identidade do vínculo; `InternshipTerm` é a fonte das condições contratuais.
- A identidade do estágio permanece separada das condições contratuais.
- A continuidade contratual do estágio é registrada exclusivamente em `InternshipTerm`.
- Não podem existir campos contratuais diretos em `Internship`.
- A empresa é fixa durante toda a vida do estágio.
- `studentId` é imutável após a criação do vínculo.
- Todos os termos do estágio pertencem ao mesmo vínculo entre aluno e empresa.
- Não pode haver sobreposição entre termos válidos do mesmo estágio.
- Não pode haver sobreposição entre períodos de estágio do mesmo aluno no domínio, ainda que pertencentes a vínculos distintos.
- Um estágio rescindido não pode receber novos termos.
- Um estágio rescindido não pode receber revisão de termos.
- A existência de termos não substitui nem redefine a identidade do estágio.
- `amendment_start_date` e `amendment_end_date` não fazem mais parte do domínio.
- `deletedAt` não substitui rescisão; ele apenas representa exclusão lógica.

## Observações

- TCE não é entidade persistida separada.
- No fluxo de TCE, o sistema cria um `Internship` e um `InternshipTerm` inicial.
- A compatibilidade temporária de contrato achatado na API não altera a separação estrutural entre `Internship` e `InternshipTerm`.
