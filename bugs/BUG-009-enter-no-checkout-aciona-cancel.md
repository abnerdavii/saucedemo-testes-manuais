# BUG-009 — Apertar Enter no formulário do checkout cancela a compra em vez de continuar

| Campo | Valor |
|---|---|
| Severidade | Média |
| Prioridade | Alta |
| Módulo | Checkout |
| Usuário | `standard_user` |
| Caso de teste | CT-020 (variação: Enter no lugar do clique em Continue) |
| Ambiente | Navegador Chromium 152 · Windows 11 · janela 1526x691 |
| Data | 04/11/2026 (primeira ocorrência em 30/10/2026) |
| Status | Aberto |

## Descrição

Na tela "Checkout: Your Information", apertar Enter em qualquer um dos campos leva o usuário de volta para o carrinho, como se ele tivesse clicado em Cancel. Os dados digitados são perdidos.

No HTML, o botão Cancel é um `<button id="cancel">` sem o atributo `type`. Sem esse atributo, o navegador trata o botão como de envio do formulário (`type="submit"`). Como o Cancel vem antes do Continue no formulário, o Enter aciona o Cancel. A correção provável é adicionar `type="button"` ao Cancel.

## Passos para reproduzir

1. Entrar com `standard_user` / `secret_sauce`.
2. Adicionar o "Sauce Labs Backpack" ao carrinho.
3. Abrir o carrinho e clicar em Checkout.
4. Preencher `Maria`, `Souza` e `15775000`.
5. Com o cursor no campo de CEP, apertar Enter.

## Resultado esperado

O formulário é enviado como se o usuário tivesse clicado em Continue, e a tela de resumo do pedido é exibida.

## Resultado atual

A tela volta para "Your Cart" (`cart.html`). Ao clicar em Checkout de novo, os três campos estão vazios. O mesmo acontece apertando Enter no campo de nome, mesmo com os outros campos vazios.

## Impacto

Quem usa o teclado para preencher formulários, prática comum, não consegue avançar no checkout com Enter e perde os dados digitados a cada tentativa. Existe alternativa: clicar em Continue funciona normalmente.

## Evidências

- [evidencias/BUG-009-enter-volta-ao-carrinho.png](../evidencias/BUG-009-enter-volta-ao-carrinho.png) (formulário preenchido antes do Enter e a tela do carrinho depois)
