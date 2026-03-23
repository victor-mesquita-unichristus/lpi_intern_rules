# 🔗 Relacionamentos e integridade

## Regras

- Não é possível criar um estágio se o aluno, o supervisor ou a empresa não existirem.
- O supervisor deve sempre estar vinculado a uma empresa existente.
- Empresas, alunos e supervisores não podem ser excluídos enquanto houver estágios vinculados a eles.
- Não é permitido mudar as referências `studentId`, `companyId` e `supervisorId` de um estágio já iniciado.
- Não haverá validação geográfica entre CEP, cidade e UF.
