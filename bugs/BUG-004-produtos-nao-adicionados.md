# BUG-004 — Alguns produtos não são adicionados ao carrinho

| Campo | Valor |
|---|---|
| Severidade | Alta |
| Prioridade | Alta |
| Módulo | Carrinho |
| Usuário | `problem_user` |
| Caso de teste | CT-016 |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

Ao clicar em "Add to cart", metade dos produtos não muda para "Remove", não altera o contador e não entra no carrinho. Não há nenhuma mensagem de erro, então o usuário não sabe que o item ficou de fora.

## Passos para reproduzir

1. Entrar com `problem_user` / `secret_sauce`, com o carrinho vazio.
2. Na listagem, clicar em "Add to cart" nos 6 produtos, de cima para baixo.
3. Observar o botão de cada produto e o contador do carrinho.

## Resultado esperado

Os 6 produtos ficam com o botão "Remove", o contador mostra 6 e todos aparecem no carrinho.

## Resultado atual

O contador mostra 3. Resultado por produto:

| Produto | Adicionado? |
|---|---|
| Sauce Labs Backpack | Sim |
| Sauce Labs Bike Light | Sim |
| Sauce Labs Bolt T-Shirt | Não |
| Sauce Labs Fleece Jacket | Não |
| Sauce Labs Onesie | Sim |
| Test.allTheThings() T-Shirt (Red) | Não |

## Impacto

O cliente pode finalizar a compra sem perceber que itens ficaram de fora, o que gera perda de venda e reclamação.

## Evidências

- [evidencias/BUG-004-produtos-nao-adicionados.png](../evidencias/BUG-004-produtos-nao-adicionados.png) (listagem depois dos 6 cliques, início e fim da página)
