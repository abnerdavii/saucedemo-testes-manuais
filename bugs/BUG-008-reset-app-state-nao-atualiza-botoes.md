# BUG-008 — "Reset App State" esvazia o carrinho, mas os botões dos produtos continuam como "Remove"

| Campo | Valor |
|---|---|
| Severidade | Média |
| Prioridade | Baixa |
| Módulo | Menu e sessão / Carrinho |
| Usuário | `standard_user` |
| Caso de teste | Encontrado na preparação do CT-017 (esvaziar o carrinho antes do caso) |
| Ambiente | Navegador Chromium 152 · Windows 11 · janela 1526x691 |
| Data | 04/11/2026 (primeira ocorrência em 03/11/2026) |
| Status | Aberto |

## Descrição

Com produtos no carrinho, a opção "Reset App State" do menu lateral esvazia o carrinho: o contador do ícone some e o conteúdo salvo no navegador (`cart-contents` no localStorage) é apagado. A listagem de produtos, porém, não é atualizada, e os botões dos itens que estavam no carrinho continuam mostrando "Remove". Os botões só voltam para "Add to cart" quando a página é recarregada.

## Passos para reproduzir

1. Entrar com `standard_user` / `secret_sauce`.
2. Na listagem, clicar em "Add to cart" no "Sauce Labs Backpack" e na "Sauce Labs Bike Light". O contador mostra 2.
3. Abrir o menu lateral e clicar em "Reset App State".
4. Fechar o menu e observar a listagem.

## Resultado esperado

O contador some e todos os botões voltam para "Add to cart", porque o carrinho está vazio.

## Resultado atual

O contador some, mas o Backpack e a Bike Light continuam com o botão "Remove". Clicar nesse "Remove" só troca o botão para "Add to cart", sem mensagem. Ao recarregar a página, os botões aparecem corretos.

## Impacto

A tela passa a informação errada sobre o carrinho: o usuário vê produtos marcados como adicionados quando o carrinho está vazio. Pode seguir para o checkout achando que tem itens.

## Evidências

- [evidencias/BUG-008-reset-nao-atualiza-botoes.png](../evidencias/BUG-008-reset-nao-atualiza-botoes.png) (antes do reset, depois do reset e depois de recarregar)
