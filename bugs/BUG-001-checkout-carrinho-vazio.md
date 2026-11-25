# BUG-001 — Compra é concluída com o carrinho vazio

| Campo | Valor |
|---|---|
| Severidade | Alta |
| Prioridade | Alta |
| Módulo | Checkout |
| Usuário | `standard_user` |
| Caso de teste | CT-025 |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

O botão Checkout continua habilitado com o carrinho vazio, e o fluxo pode ser levado até o fim. O sistema exibe a confirmação de pedido para uma compra sem nenhum item, com total de $0.00.

## Passos para reproduzir

1. Acessar https://www.saucedemo.com e entrar com `standard_user` / `secret_sauce`.
2. Com o carrinho vazio, clicar no ícone do carrinho.
3. Clicar em Checkout.
4. Preencher `Maria`, `Souza`, `15775000` e clicar em Continue.
5. Na tela de resumo, clicar em Finish.

## Resultado esperado

O sistema não permite iniciar o checkout sem itens: o botão Checkout fica desabilitado ou uma mensagem informa que o carrinho está vazio.

## Resultado atual

O checkout segue normalmente, sem nenhum aviso. O resumo não lista itens e mostra "Item total: $0", "Tax: $0.00" e "Total: $0.00". Depois do Finish, a tela "Thank you for your order!" é exibida.

O valor "Item total: $0" aparece sem centavos, diferente dos outros valores da tela.

## Impacto

Em uma loja real, gera pedidos vazios no sistema, que podem disparar e-mails de confirmação, entrar em relatórios de venda e chegar à equipe de expedição.

## Evidências

- [evidencias/BUG-001-compra-com-carrinho-vazio.png](../evidencias/BUG-001-compra-com-carrinho-vazio.png) (carrinho vazio, resumo zerado e confirmação do pedido)
