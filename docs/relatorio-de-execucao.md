# Relatório de execução — SauceDemo

| Item | Detalhe |
|---|---|
| Rodada | 1 |
| Período | 30/10/2026 a 24/11/2026 |
| Responsável | Abner Davi |
| Aplicação | https://www.saucedemo.com |

## Ambiente

| Etapas | Datas | Navegador | Sistema | Janela |
|---|---|---|---|---|
| 1 a 4 (smoke, login, produtos, carrinho) | 30/10 a 04/11/2026 | Navegador baseado em Chromium 152 | Windows 11 | 1526x691 |
| 5 a 9 (checkout, sessão, perfis, desempenho, exploratória) | 24/11/2026 | Brave 158 (Chromium 158) | Windows | 1440x681 |

Os bugs foram reproduzidos no ambiente indicado em cada relatório. O BUG-007 apareceu nos dois navegadores.

## Resultado geral

| Módulo | Planejados | Executados | Passou | Falhou | Bloqueado |
|---|---|---|---|---|---|
| Login | 8 | 8 | 7 | 1 | 0 |
| Produtos | 6 | 6 | 3 | 3 | 0 |
| Carrinho | 5 | 5 | 4 | 1 | 0 |
| Checkout | 7 | 7 | 5 | 2 | 0 |
| Menu e sessão | 2 | 2 | 2 | 0 | 0 |
| **Total** | **28** | **28** | **21** | **7** | **0** |

Um caso que passou com `standard_user` e falhou com `problem_user` foi contado como **Falhou**. É o caso do CT-010, CT-011, CT-012, CT-016 e CT-023. Sem contar as falhas exclusivas do `problem_user`, seriam 26 casos com Passou e 2 com Falhou: o CT-008, que usa o `performance_glitch_user`, e o CT-025.

## Defeitos

12 defeitos registrados, todos abertos.

| ID | Título | Severidade | Prioridade | Usuário |
|---|---|---|---|---|
| [BUG-001](../bugs/BUG-001-checkout-carrinho-vazio.md) | Compra concluída com carrinho vazio | Alta | Alta | `standard_user` |
| [BUG-002](../bugs/BUG-002-checkout-sem-validacao-de-formato.md) | Campos do checkout aceitam qualquer formato, inclusive só espaços | Média | Média | `standard_user` |
| [BUG-003](../bugs/BUG-003-sobrenome-nao-aceita-digitacao.md) | Sobrenome não aceita digitação e impede a compra | Crítica | Alta | `problem_user` |
| [BUG-004](../bugs/BUG-004-produtos-nao-adicionados.md) | Alguns produtos não são adicionados ao carrinho | Alta | Alta | `problem_user` |
| [BUG-005](../bugs/BUG-005-ordenacao-nao-funciona.md) | Ordenação não altera a lista | Média | Média | `problem_user` |
| [BUG-006](../bugs/BUG-006-imagens-incorretas.md) | Todos os produtos exibem a mesma imagem | Média | Média | `problem_user` |
| [BUG-007](../bugs/BUG-007-mensagem-de-erro-vaza-da-caixa.md) | Mensagem de erro do login vaza para fora da caixa | Baixa | Média | Todos |
| [BUG-008](../bugs/BUG-008-reset-app-state-nao-atualiza-botoes.md) | Reset App State não atualiza os botões da listagem | Média | Baixa | `standard_user` |
| [BUG-009](../bugs/BUG-009-enter-no-checkout-aciona-cancel.md) | Enter no formulário do checkout aciona o Cancel | Média | Alta | `standard_user` |
| [BUG-010](../bugs/BUG-010-login-lento-performance-glitch-user.md) | Login do `performance_glitch_user` leva cerca de 5 segundos | Média | Média | `performance_glitch_user` |
| [BUG-011](../bugs/BUG-011-carrinho-compartilhado-entre-usuarios.md) | Carrinho de um usuário aparece para outro no mesmo navegador | Alta | Alta | Vários |
| [BUG-012](../bugs/BUG-012-checkout-pula-dados-pela-url.md) | Pedido concluído sem os dados do comprador, pela URL | Alta | Alta | `standard_user` |

| Severidade | Quantidade |
|---|---|
| Crítica | 1 |
| Alta | 4 |
| Média | 6 |
| Baixa | 1 |

Sete defeitos (BUG-001, 002, 007, 008, 009, 011 e 012) acontecem com o `standard_user`, o perfil de referência, ou com qualquer usuário. Os outros cinco (BUG-003 a 006 e BUG-010) são próprios dos perfis com falhas simuladas.

## Sessão exploratória

| Item | Detalhe |
|---|---|
| Missão | Explorar o checkout em busca de entradas que o sistema deveria recusar |
| Data | 24/11/2026, das 22:23 às 22:26 (o plano previa até 30 minutos) |
| Usuário | `standard_user` |
| Explorado | Números e símbolos nos nomes, letras e um único dígito no CEP, campos só com espaços, nome com 288 caracteres, ordem da tecla Tab, botão voltar do navegador durante o checkout, acesso direto às URLs das etapas do checkout |
| Encontrado | BUG-002 (confirmado, com novos valores aceitos) e BUG-012 (novo) |
| Sem defeito | A ordem do Tab está correta: nome → sobrenome → CEP → Cancel → Continue |
| Dúvidas para o time | O CEP deve seguir algum formato específico? Qual o tamanho máximo esperado para os nomes? O carrinho vazio deveria bloquear o botão Checkout ou mostrar uma mensagem? |

## Observações

- **Formulário apagado ao voltar:** voltar com o navegador do resumo para a tela de dados apaga o formulário, e o comprador precisa digitar tudo de novo.
- **Valor sem centavos:** no resumo de um pedido vazio, o "Item total" aparece como "$0", sem centavos, diferente do imposto e do total ("$0.00"). Registrado dentro do BUG-001.
- **Cookie do usuário bloqueado:** um login negado do `locked_out_user` grava um cookie de sessão com o nome desse usuário, mas esse cookie não dá acesso à loja. Não foi tratado como defeito.
- **Rolagem após o Cancel:** depois do Cancel no resumo, a listagem abre rolada até o fim da página, na mesma posição em que estava a tela anterior.
- **Funções fora do escopo:** o menu "Dynamic Catalog" e o botão "Generate PDF order" apareceram durante a execução e ficaram fora desta rodada, como registrado no plano.

## Critérios de saída

| Critério | Situação |
|---|---|
| 100% dos casos de prioridade alta executados | Atendido: os 11 casos de prioridade alta foram executados |
| Todos os defeitos registrados com evidência | Atendido: 12 relatórios, cada um com print |
| Nenhum defeito crítico sem registro | Atendido: o único crítico (BUG-003) está registrado |

## Conclusão

O fluxo principal de compra funciona para o `standard_user`: login, listagem, carrinho, cálculo do total e conclusão do pedido passaram. Mesmo assim, a loja não deveria ser liberada nesse estado, por causa de três falhas de regra de negócio que atingem qualquer cliente: pedido com carrinho vazio (BUG-001), pedido sem dados de entrega acessando o resumo pela URL (BUG-012) e carrinho que passa de um usuário para outro no mesmo navegador (BUG-011). No `problem_user`, a compra fica totalmente bloqueada pelo BUG-003. A recomendação é corrigir primeiro BUG-001, BUG-011, BUG-012 e BUG-003, junto com o BUG-009, que tem correção simples e afeta quem usa o teclado, e depois reexecutar os casos de carrinho e checkout.
