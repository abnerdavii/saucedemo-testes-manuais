# BUG-012 — Pedido pode ser concluído sem os dados do comprador, acessando o resumo pela URL

| Campo | Valor |
|---|---|
| Severidade | Alta |
| Prioridade | Alta |
| Módulo | Checkout |
| Usuário | `standard_user` |
| Origem | Sessão exploratória do checkout |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

As telas do checkout não verificam se a etapa anterior foi concluída. Abrindo `checkout-step-two.html` direto pela barra de endereço, o resumo do pedido aparece sem que o comprador tenha informado nome, sobrenome e CEP, e o pedido pode ser finalizado. A página de confirmação (`checkout-complete.html`) também abre direto, mesmo sem pedido.

## Passos para reproduzir

1. Entrar com `standard_user` / `secret_sauce`, com um produto no carrinho.
2. Sem passar pela tela de dados, acessar `https://www.saucedemo.com/checkout-step-two.html` pela barra de endereço.
3. Clicar em Finish.

## Resultado esperado

O sistema redireciona para a tela de dados (`checkout-step-one.html`) e só mostra o resumo depois que os dados obrigatórios forem informados.

## Resultado atual

O resumo é exibido com o item e o total ($32.39), e o Finish leva à tela "Thank you for your order!".

Acessando `https://www.saucedemo.com/checkout-complete.html` direto, com um item no carrinho, a tela de agradecimento também aparece, mas o item continua no carrinho.

## Impacto

Um pedido pode ser registrado sem nenhuma informação de entrega. A validação de campos obrigatórios da tela de dados (CT-022 a CT-024) perde o efeito, porque a etapa pode ser pulada.

## Evidências

- [evidencias/BUG-012-resumo-sem-dados.png](../evidencias/BUG-012-resumo-sem-dados.png) (resumo aberto pela URL, pedido concluído e confirmação aberta direto)
