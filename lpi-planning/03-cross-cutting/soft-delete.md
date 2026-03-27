# Soft Delete

## Propósito

Definir a direção transversal de exclusão para registros persistidos no sistema.

## Direção atual

- `deletedAt` é o padrão preferencial transversal do sistema para exclusão lógica.
- Entidades ainda não consolidadas nesse padrão devem ser tratadas como pendentes de migração ou consolidação.

## Regras canônicas

- Soft delete usa `deletedAt` como modelo canônico preferencial.
- Listagens padrão ignoram registros com `deletedAt` preenchido.
- Seleções e associações ignoram registros com `deletedAt` preenchido.
- Referências históricas continuam visíveis quando já fazem parte de registros existentes.
- Exclusão física deve ser evitada quando o histórico de negócio precisar ser preservado.

## Estado atual de consolidação

- Agente Integrador: confirmado com `deletedAt`.
- `Internship`: confirmado com `deletedAt`.
- `InternshipTerm`: confirmado com `deletedAt`.
- Empresa: `PENDENTE DE DECISÃO`.
- Aluno: `PENDENTE DE DECISÃO`.
- Supervisor: `PENDENTE DE DECISÃO`.
- Usuário: `PENDENTE DE DECISÃO`.
- Curso: `PENDENTE DE DECISÃO`.

## Implicações operacionais

- Listagens padrão devem ocultar registros com `deletedAt` preenchido.
- Componentes de seleção não devem oferecer registros removidos logicamente.
- Registros historicamente vinculados podem continuar aparecendo em telas de detalhe para auditoria e rastreabilidade.
- Termos revisados não devem ser removidos logicamente apenas por terem perdido vigência.
- Perda de vigência lógica por revisão não se confunde com `deletedAt`.

## Observação

- `Internship` e `InternshipTerm` já estão consolidados neste padrão.
- Onde a consolidação de outras entidades ainda não foi formalmente confirmada, a documentação deve permanecer marcada como `PENDENTE DE DECISÃO`.
