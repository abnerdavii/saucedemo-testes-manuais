# BUG-007 — Mensagem de erro do login vaza para fora da caixa vermelha

| Campo | Valor |
|---|---|
| Severidade | Baixa |
| Prioridade | Média |
| Módulo | Login |
| Usuário | `standard_user` (ocorre com qualquer usuário) |
| Caso de teste | CT-002, CT-003, CT-007 |
| Ambiente | Google Chrome 156.0.8078.48 · Windows 11 · layout de desktop (também ocorre em 1280x800 e 1920x1080) |
| Data | 03/11/2026 |
| Status | Aberto |

## Descrição

Na tela de login, quando a mensagem de erro é longa, o texto quebra em três linhas e passa da borda da caixa vermelha: a primeira linha fica por cima do campo de senha e a última por cima do botão Login. Parte do texto fica ilegível.

A caixa (`.error-message-container`) tem altura fixa de 45px. O texto (`h3`, altura de linha de 20px) ocupa 60px quando quebra em três linhas e não cabe. Mensagens curtas, como "Username is required", ficam em uma linha e não são afetadas.

## Passos para reproduzir

1. Acessar https://www.saucedemo.com em uma janela de desktop.
2. Informar `standard_user` no usuário e `senha123` na senha.
3. Clicar em Login.

## Resultado esperado

A caixa vermelha cresce junto com o texto, e a mensagem inteira fica visível dentro dela.

## Resultado atual

A mensagem "Epic sadface: Username and password do not match any user in this service" ocupa três linhas, e a primeira e a última ficam para fora da caixa, cortadas pela borda.

O mesmo acontece com a mensagem do acesso direto sem login ("You can only access '/inventory.html' when you are logged in.").

## Impacto

Afeta as mensagens de erro mais comuns do login, as que aparecem quando o usuário erra a senha ou tenta entrar numa página sem estar logado. O usuário consegue tentar de novo, mas pode não entender o motivo do erro.

## Evidências

- [evidencias/BUG-007-mensagem-vazando.png](../evidencias/BUG-007-mensagem-vazando.png) (recorte ampliado do CT-002)
- [evidencias/BUG-007-print-original.png](../evidencias/BUG-007-print-original.png) (primeira ocorrência, senha inválida com `standard_user`)
- [evidencias/CT-007-acesso-sem-login.png](../evidencias/CT-007-acesso-sem-login.png) (mesma falha na mensagem de acesso sem login)
