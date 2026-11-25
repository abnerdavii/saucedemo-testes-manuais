# BUG-006 — Todos os produtos exibem a mesma imagem

| Campo | Valor |
|---|---|
| Severidade | Média |
| Prioridade | Média |
| Módulo | Produtos |
| Usuário | `problem_user` |
| Caso de teste | CT-010 |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

Na listagem, os 6 produtos aparecem com a mesma imagem, a foto de um cachorro, que não corresponde a nenhum deles. Todas as imagens apontam para o mesmo arquivo, `/assets/sl-404-Cq1a9k9X.jpg`.

## Passos para reproduzir

1. Entrar com `problem_user` / `secret_sauce`.
2. Observar a imagem de cada produto na listagem.

## Resultado esperado

Cada produto exibe a própria imagem, igual à vista com `standard_user`.

## Resultado atual

Os 6 produtos exibem a mesma imagem de um cachorro. O nome do arquivo (`sl-404`) indica uma imagem de erro "não encontrado".

## Impacto

O cliente não consegue identificar visualmente o produto e pode desistir da compra ou comprar o item errado.

## Evidências

- [evidencias/BUG-006-imagens-iguais.png](../evidencias/BUG-006-imagens-iguais.png) (listagem com `problem_user` e, para comparação, com `standard_user`)
