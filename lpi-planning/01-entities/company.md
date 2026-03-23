# Empresa

## Propósito

Representa a organização que oferece vagas de estágio.

## Campos relevantes

- `legal_name`
- `fantasy_name`
- `cnpj`
- `sector`
- `business_area`
- Campos de endereço
- Nome do representante
- Cargo do representante

## Regras de cadastro

- `legal_name`, `fantasy_name`, `cnpj`, `sector` e `business_area` são obrigatórios.
- `cnpj` deve ser único e válido.
- `cnpj` é armazenado apenas com dígitos.
- `sector` aceita apenas `public` ou `private`.
- O estado deve usar UF com 2 letras maiúsculas.
- O CEP deve seguir o formato brasileiro.

## Regras de edição

- Os dados da empresa podem ser editados desde que as regras de unicidade e formato continuem válidas.
- Não há validação geográfica cruzada entre CEP, cidade e estado.

## Regras de exclusão

- Uma empresa não pode ser excluída se houver supervisores vinculados a ela.
- Uma empresa não pode ser excluída se houver estágios vinculados a ela.

## Relacionamentos

- Uma empresa possui muitos supervisores.
- Uma empresa possui muitos estágios.

## Invariantes

- Uma empresa referenciada por supervisor ou estágio deve existir.
- A identidade da empresa é ancorada por um `cnpj` único.

## Observações de MVP

- Estados de ciclo de vida como empresa encerrada ou inativa estão fora do escopo do MVP.
