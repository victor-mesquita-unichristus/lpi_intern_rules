# 🔗 Relacionamentos e integridade

## Regras

- Não é possível criar um estágio se o aluno, o supervisor ou a empresa não existirem.
- O supervisor deve sempre estar vinculado a uma empresa existente.
- O supervisor informado em um `InternshipTerm` deve pertencer à mesma empresa do `Internship` associado.
- Empresas, alunos e supervisores não podem ser excluídos enquanto houver estágios ou termos vinculados a eles.
- Não é permitido mudar as referências `studentId` e `companyId` de um `Internship` já criado.
- Mudanças de supervisor não ocorrem por mutação direta de `Internship`; elas ocorrem por fluxo sobre o termo.
- Não haverá validação geográfica entre CEP, cidade e UF.
