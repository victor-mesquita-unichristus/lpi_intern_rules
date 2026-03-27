# Soft Delete

## Propósito

Definir a direção transversal de exclusão para registros persistidos no sistema.

## Direção atual

- `deletedAt` é o padrão preferencial transversal do sistema para exclusão lógica.
- Entidades ainda não consolidadas nesse padrão devem ser tratadas como pendentes de migração ou consolidação.
- Quando a consolidação de uma entidade ainda não estiver confirmada, a documentação deve marcar explicitamente `PENDENTE DE DECISÃO`.

## Regras canônicas

- Soft delete usa `deletedAt` como modelo canônico preferencial.
- Listagens padrão ignoram registros com `deletedAt` preenchido.
- Seleções e associações ignoram registros com `deletedAt` preenchido.
- Referências históricas continuam visíveis quando já fazem parte de registros existentes.
- Exclusão física deve ser evitada quando o histórico de negócio precisar ser preservado.

## Estado atual de consolidação

- Agente Integrador: confirmado com `deletedAt`.
- `Internship`: `PENDENTE DE DECISÃO`.
- `InternshipTerm`: `PENDENTE DE DECISÃO`.
- Empresa: `PENDENTE DE DECISÃO`.
- Aluno: `PENDENTE DE DECISÃO`.
- Supervisor: `PENDENTE DE DECISÃO`.
- Usuário: `PENDENTE DE DECISÃO`.
- Curso: `PENDENTE DE DECISÃO`.

## Implicações operacionais

- Listagens padrão devem ocultar registros com `deletedAt` preenchido.
- Componentes de seleção não devem oferecer registros removidos logicamente.
- Registros historicamente vinculados podem continuar aparecendo em telas de detalhe para auditoria e rastreabilidade.

## Observação

- A direção de soft delete não autoriza presumir que todas as entidades já estejam consolidadas com `deletedAt` hoje.
- Onde essa consolidação não foi formalmente confirmada, a documentação deve permanecer marcada como `PENDENTE DE DECISÃO`.
