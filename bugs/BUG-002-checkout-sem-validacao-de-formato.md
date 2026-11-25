# BUG-002 — Campos do checkout aceitam qualquer formato, inclusive só espaços

| Campo | Valor |
|---|---|
| Severidade | Média |
| Prioridade | Média |
| Módulo | Checkout |
| Usuário | `standard_user` |
| Origem | Sessão exploratória do checkout |
| Ambiente | Brave 158 (Chromium 158) · Windows · janela 1440x681 |
| Data | 24/11/2026 |
| Status | Aberto |

## Descrição

Os campos de dados do comprador só verificam se estão vazios. Não há validação de formato nem de tamanho: os campos de nome aceitam números e símbolos, o CEP aceita letras e um único dígito, e os três campos aceitam valores formados só por espaços, o que contorna a regra de campo obrigatório.

## Passos para reproduzir

1. Entrar com `standard_user` e adicionar qualquer produto ao carrinho.
2. Abrir o carrinho e clicar em Checkout.
3. Preencher First Name com `123!@#`, Last Name com `%%%` e Zip/Postal Code com `abc`.
4. Clicar em Continue.

## Resultado esperado

O sistema recusa os dados e informa qual campo está em formato inválido.

## Resultado atual

O sistema aceita os valores e avança para o resumo do pedido. A compra pode ser finalizada.

## Valores testados

| Campo | Valor | Aceito? |
|---|---|---|
| First Name | `123!@#` | Sim |
| Last Name | `%%%` | Sim |
| Zip/Postal Code | `abc` | Sim |
| Os três campos | três espaços | Sim |
| First Name | 288 caracteres | Sim |
| Zip/Postal Code | `1` | Sim |

Os campos não têm limite de tamanho (`maxlength`) nem padrão de formato (`pattern`).

## Impacto

Em uma loja real, pedidos com nome ou endereço inválido não podem ser entregues e geram custo de suporte e reenvio. O caso dos espaços mostra que a validação de campo obrigatório pode ser contornada.

## Evidências

- [evidencias/BUG-002-dados-invalidos.png](../evidencias/BUG-002-dados-invalidos.png) (números, símbolos e letras no CEP)
- [evidencias/BUG-002-so-espacos.png](../evidencias/BUG-002-so-espacos.png) (campos só com espaços)
