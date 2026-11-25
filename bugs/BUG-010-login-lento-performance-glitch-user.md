# BUG-010 — Login do `performance_glitch_user` leva cerca de 5 segundos

| Campo | Valor |
|---|---|
| Severidade | Média |
| Prioridade | Média |
| Módulo | Login |
| Usuário | `performance_glitch_user` |
| Caso de teste | CT-008 |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

Depois do clique em Login, a tela fica parada na página de login por cerca de 5 segundos antes de mostrar a lista de produtos. Não há indicador de carregamento. O limite definido no CT-008 é de 3 segundos.

## Passos para reproduzir

1. Acessar https://www.saucedemo.com.
2. Informar `performance_glitch_user` / `secret_sauce`.
3. Clicar em Login e medir o tempo até a lista de produtos aparecer.

## Resultado esperado

O login é concluído em até 3 segundos, como acontece com `standard_user`.

## Resultado atual

| Usuário | Execução | Tempo |
|---|---|---|
| `performance_glitch_user` | 1 | 5,03 s |
| `performance_glitch_user` | 2 | 5,03 s |
| `performance_glitch_user` | 3 | 5,03 s |
| `performance_glitch_user` | 4 | 5,03 s |
| `standard_user` | referência | 0,02 s |

O tempo foi medido no próprio navegador com `performance.now()`, do clique em Login até os 6 produtos aparecerem na tela. O resultado igual nas quatro execuções indica um atraso fixo, e não oscilação de rede.

## Impacto

Sem indicador de carregamento, o usuário pode achar que o clique não funcionou e clicar de novo ou desistir.

## Evidências

- [evidencias/BUG-010-login-lento.png](../evidencias/BUG-010-login-lento.png) (medições e tela depois do login)
