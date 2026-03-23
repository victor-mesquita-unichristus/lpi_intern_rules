# 🏢 Empresa (Company)

## Regras gerais

- O CNPJ é único e deve ser válido.
- Para persistência, o CNPJ é armazenado apenas com números, sem pontos, barras ou hífens.

## Campos obrigatórios

- Razão social (`legal_name`)
- Nome fantasia (`fantasy_name`)
- CNPJ (`cnpj`)
- Setor (`sector`)
- Área de atuação (`business_area`)
- Endereço: rua, bairro, CEP, cidade e estado
- Representante: nome e cargo

## Validações

- O setor pode ser apenas **público** ou **privado**.
- O estado (UF) deve conter duas letras maiúsculas.
- O CEP deve estar no formato brasileiro, por exemplo: `12345-678` ou `12345678`.
- Não será feita validação geográfica, ou seja, não há checagem cruzada entre CEP, cidade e UF.

## Restrições

- Uma empresa não pode ser excluída se houver supervisores ou estágios vinculados.
- Alterações sobre empresa encerrada ou inativa ficam fora do escopo do MVP.
