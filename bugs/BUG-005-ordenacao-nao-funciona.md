# BUG-005 — Ordenação de produtos não altera a lista

| Campo | Valor |
|---|---|
| Severidade | Média |
| Prioridade | Média |
| Módulo | Produtos |
| Usuário | `problem_user` |
| Casos de teste | CT-011, CT-012 |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

Escolher uma opção no seletor de ordenação não tem efeito: o seletor volta para "Name (A to Z)" e a lista permanece na ordem inicial. Nenhuma mensagem é exibida.

## Passos para reproduzir

1. Entrar com `problem_user` / `secret_sauce`.
2. Abrir o seletor de ordenação e escolher "Name (Z to A)".
3. Observar o seletor e a ordem dos produtos.
4. Repetir com "Price (low to high)".

## Resultado esperado

A lista é reordenada conforme a opção escolhida. Em "Name (Z to A)", o primeiro produto é o Test.allTheThings() T-Shirt (Red); em "Price (low to high)", é o Sauce Labs Onesie ($7.99).

## Resultado atual

Nas duas opções, o seletor volta a mostrar "Name (A to Z)" e a lista continua começando pelo Sauce Labs Backpack. Os preços ficam na ordem original: $29.99, $9.99, $15.99, $49.99, $7.99, $15.99.

## Comparação

Com `standard_user`, as quatro opções de ordenação funcionam (CT-011 e CT-012 passaram).

## Impacto

O usuário perde uma forma de encontrar produtos. Existe alternativa (procurar na lista), por isso a severidade é média.

## Evidências

- [evidencias/BUG-005-ordenacao-nao-funciona.png](../evidencias/BUG-005-ordenacao-nao-funciona.png) (listagem depois de escolher Name (Z to A) e Price (low to high))
