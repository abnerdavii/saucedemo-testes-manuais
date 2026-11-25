# BUG-003 — Campo de sobrenome não aceita digitação e impede a compra

| Campo | Valor |
|---|---|
| Severidade | Crítica |
| Prioridade | Alta |
| Módulo | Checkout |
| Usuário | `problem_user` |
| Caso de teste | CT-023 |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

Na tela de dados do checkout, o texto digitado no campo Last Name não fica nele. Cada tecla substitui o conteúdo do campo First Name, que termina com a última letra digitada. O sobrenome continua vazio e a validação de campo obrigatório impede o avanço. Não existe caminho alternativo para concluir a compra.

## Passos para reproduzir

1. Entrar com `problem_user` / `secret_sauce`.
2. Adicionar um produto ao carrinho.
3. Abrir o carrinho e clicar em Checkout.
4. Clicar no campo First Name e digitar `Maria`.
5. Clicar no campo Last Name e digitar `Souza`.
6. Preencher Zip/Postal Code com `15775000` e clicar em Continue.

## Resultado esperado

Cada campo mantém o valor digitado e o usuário avança para o resumo do pedido.

## Resultado atual

Depois do passo 5, o campo First Name mostra só `a` (a última letra de "Souza") e o Last Name continua vazio. Ao clicar em Continue, aparece "Error: Last Name is required".

## Comparação

O mesmo fluxo com `standard_user` funciona normalmente (CT-023 com `standard_user` passou), o que confirma que a falha é do comportamento da interface para esse perfil.

## Impacto

Bloqueia 100% das compras para esse perfil de usuário.

## Evidências

- [evidencias/BUG-003-sobrenome-nao-aceita-digitacao.png](../evidencias/BUG-003-sobrenome-nao-aceita-digitacao.png) (campos depois da digitação e mensagem de erro)
