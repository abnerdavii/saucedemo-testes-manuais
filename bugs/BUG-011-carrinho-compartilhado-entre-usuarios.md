# BUG-011 — Carrinho de um usuário aparece para outro usuário no mesmo navegador

| Campo | Valor |
|---|---|
| Severidade | Alta |
| Prioridade | Alta |
| Módulo | Carrinho / Menu e sessão |
| Usuário | `standard_user` e `performance_glitch_user` |
| Origem | Encontrado durante a etapa 7 (comparação de perfis) e reproduzido em seguida |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

O carrinho não é limpo no logout nem separado por usuário. Os itens ficam salvos no navegador (`cart-contents` no localStorage) e aparecem para qualquer usuário que entrar depois no mesmo navegador.

## Passos para reproduzir

1. Entrar com `standard_user` / `secret_sauce`.
2. Esvaziar o carrinho e adicionar só o "Sauce Labs Backpack". O contador mostra 1.
3. Abrir o menu lateral e clicar em Logout.
4. Entrar com `performance_glitch_user` / `secret_sauce`.
5. Observar o contador e abrir o carrinho.

## Resultado esperado

O carrinho do segundo usuário começa vazio, ou mostra só os itens dele.

## Resultado atual

O contador mostra 1 logo depois do login, e o carrinho contém o "Sauce Labs Backpack" adicionado pelo `standard_user`.

O mesmo aconteceu antes, de forma espontânea: ao entrar com `problem_user`, o carrinho já tinha os dois itens deixados pelo `standard_user`.

## Impacto

Num computador compartilhado, um cliente vê e pode comprar os itens escolhidos por outra pessoa. Além de causar compras erradas, expõe o que outro cliente estava comprando.

## Evidências

- [evidencias/BUG-011-carrinho-compartilhado.png](../evidencias/BUG-011-carrinho-compartilhado.png) (carrinho do `standard_user` e o mesmo carrinho com `performance_glitch_user`)
