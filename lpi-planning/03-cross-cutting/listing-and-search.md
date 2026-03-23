# Listing and Search

## Propósito

Padronizar o comportamento de listagem e busca entre entidades.

## Regras

- Listagens devem ser paginadas.
- Listagens padrão devem preferir apenas registros ativos.
- A busca deve suportar correspondência parcial quando isso fizer sentido.
- Filtros de busca e listagem devem ser consistentes com as regras de ciclo de vida das entidades.
- Registros inativos podem ser expostos apenas em contextos administrativos.

## Casos conhecidos

- Cursos: busca por nome.
- Agentes integradores: busca por nome.
- Outras entidades podem definir identificadores pesquisáveis adicionais.
