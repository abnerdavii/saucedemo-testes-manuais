# Bugs

12 defeitos registrados na rodada 1 (30/10/2026 a 24/11/2026). Todos estão abertos.

| ID | Título | Severidade | Prioridade | Usuário | Origem |
|---|---|---|---|---|---|
| [BUG-001](BUG-001-checkout-carrinho-vazio.md) | Compra concluída com carrinho vazio | Alta | Alta | `standard_user` | CT-025 |
| [BUG-002](BUG-002-checkout-sem-validacao-de-formato.md) | Campos do checkout aceitam qualquer formato, inclusive só espaços | Média | Média | `standard_user` | Sessão exploratória |
| [BUG-003](BUG-003-sobrenome-nao-aceita-digitacao.md) | Sobrenome não aceita digitação e impede a compra | Crítica | Alta | `problem_user` | CT-023 |
| [BUG-004](BUG-004-produtos-nao-adicionados.md) | Alguns produtos não são adicionados ao carrinho | Alta | Alta | `problem_user` | CT-016 |
| [BUG-005](BUG-005-ordenacao-nao-funciona.md) | Ordenação não altera a lista | Média | Média | `problem_user` | CT-011, CT-012 |
| [BUG-006](BUG-006-imagens-incorretas.md) | Todos os produtos exibem a mesma imagem | Média | Média | `problem_user` | CT-010 |
| [BUG-007](BUG-007-mensagem-de-erro-vaza-da-caixa.md) | Mensagem de erro do login vaza para fora da caixa | Baixa | Média | Todos | CT-002, CT-003, CT-007 |
| [BUG-008](BUG-008-reset-app-state-nao-atualiza-botoes.md) | Reset App State não atualiza os botões da listagem | Média | Baixa | `standard_user` | Preparação do CT-017 |
| [BUG-009](BUG-009-enter-no-checkout-aciona-cancel.md) | Enter no formulário do checkout aciona o Cancel | Média | Alta | `standard_user` | CT-020 (variação) |
| [BUG-010](BUG-010-login-lento-performance-glitch-user.md) | Login do `performance_glitch_user` leva cerca de 5 segundos | Média | Média | `performance_glitch_user` | CT-008 |
| [BUG-011](BUG-011-carrinho-compartilhado-entre-usuarios.md) | Carrinho de um usuário aparece para outro no mesmo navegador | Alta | Alta | Vários | Etapa 7 |
| [BUG-012](BUG-012-checkout-pula-dados-pela-url.md) | Pedido concluído sem os dados do comprador, pela URL | Alta | Alta | `standard_user` | Sessão exploratória |

## Por severidade

| Severidade | Quantidade |
|---|---|
| Crítica | 1 |
| Alta | 4 |
| Média | 6 |
| Baixa | 1 |
| **Total** | **12** |

Modelo usado nos relatórios: [TEMPLATE.md](TEMPLATE.md)
