# Soft Delete

## Propósito

Definir a direção sistêmica de exclusão para registros persistidos.

## Abrangência

- Soft delete com `deletedAt` é a direção preferencial do sistema sempre que possível.
- Essa direção já está explícita para Agente Integrador.
- O material existente ainda descreve comportamentos mais antigos de exclusão para algumas entidades e precisa de consolidação.

## Regras

- Soft delete deve preferir `deletedAt` como modelo canônico.
- Registros removidos logicamente não aparecem na listagem padrão.
- Registros removidos logicamente não podem ser selecionados em fluxos de criação.
- Referências históricas continuam visíveis em registros já existentes.
- A exclusão física deve ser evitada quando o histórico de negócio precisar ser preservado.

## Estado atual de consolidação

- Agente Integrador já está alinhado com `deletedAt`.
- Curso atualmente referencia estado inativo e deve ser alinhado quando possível.
- Estágio tem restrições antigas de exclusão documentadas, mas a direção atual é alinhá-lo ao soft delete quando possível.
- `PENDENTE DE DECISÃO`: confirmar se Empresa, Aluno, Supervisor e Usuário já seguem ou seguirão o mesmo modelo com `deletedAt` no MVP.

## Implicações operacionais

- Listagens padrão devem ocultar registros removidos logicamente.
- Componentes de seleção, como o dropdown de agente integrador no TCE, não devem oferecer registros removidos logicamente.
- Telas de detalhe histórico podem continuar exibindo registros excluídos que já estavam vinculados, para auditoria e rastreabilidade.
