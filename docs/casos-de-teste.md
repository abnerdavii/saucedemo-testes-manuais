# Casos de teste — SauceDemo

Senha de todos os usuários: `secret_sauce`. Quando não indicado, o usuário é o `standard_user`.

**Status:** Passou · Falhou · Bloqueado · A executar

## Login

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Prioridade | Status |
|---|---|---|---|---|---|---|
| CT-001 | Login com credenciais válidas | Estar na tela de login | 1. Informar `standard_user`<br>2. Informar a senha<br>3. Clicar em Login | Usuário é levado para a página de produtos (`/inventory.html`) | Alta | Passou ([evidência](../evidencias/CT-001-login-valido.png)) |
| CT-002 | Login com senha incorreta | Estar na tela de login | 1. Informar `standard_user`<br>2. Informar a senha `senha123`<br>3. Clicar em Login | Mensagem "Username and password do not match any user in this service" e o usuário continua na tela de login | Alta | Passou ([evidência](../evidencias/CT-002-senha-incorreta.png)) |
| CT-003 | Login com usuário inexistente | Estar na tela de login | 1. Informar `usuario_teste`<br>2. Informar a senha<br>3. Clicar em Login | Mesma mensagem do CT-002, sem indicar qual dos dois campos está errado | Média | Passou ([evidência](../evidencias/CT-003-usuario-inexistente.png)) |
| CT-004 | Login com usuário em branco | Estar na tela de login | 1. Deixar o usuário vazio<br>2. Informar a senha<br>3. Clicar em Login | Mensagem "Username is required" | Média | Passou ([evidência](../evidencias/CT-004-usuario-em-branco.png)) |
| CT-005 | Login com senha em branco | Estar na tela de login | 1. Informar `standard_user`<br>2. Deixar a senha vazia<br>3. Clicar em Login | Mensagem "Password is required" | Média | Passou ([evidência](../evidencias/CT-005-senha-em-branco.png)) |
| CT-006 | Login com usuário bloqueado | Estar na tela de login | 1. Informar `locked_out_user`<br>2. Informar a senha<br>3. Clicar em Login | Mensagem "Sorry, this user has been locked out." e acesso negado | Alta | Passou ([evidência](../evidencias/CT-006-usuario-bloqueado.png)) |
| CT-007 | Acesso direto a página interna sem login | Não estar logado | 1. Acessar `https://www.saucedemo.com/inventory.html` pela barra de endereço | Usuário volta para a tela de login com mensagem informando que precisa estar logado | Alta | Passou ([evidência](../evidencias/CT-007-acesso-sem-login.png)) |
| CT-008 | Tempo de login com `performance_glitch_user` | Estar na tela de login | 1. Informar `performance_glitch_user`<br>2. Informar a senha<br>3. Clicar em Login e cronometrar | Login concluído em até 3 segundos | Baixa | A executar |

## Produtos

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Prioridade | Status |
|---|---|---|---|---|---|---|
| CT-009 | Exibição da lista de produtos | Logado | 1. Observar a página de produtos | 6 produtos exibidos, cada um com imagem, nome, descrição, preço e botão "Add to cart" | Alta | Passou ([evidência](../evidencias/CT-009-lista-de-produtos.png)) |
| CT-010 | Imagem correspondente ao produto | Logado | 1. Comparar a imagem de cada produto com o nome<br>2. Repetir com `problem_user` | Cada produto mostra a própria imagem | Média | A executar |
| CT-011 | Ordenar por nome (A a Z e Z a A) | Logado | 1. Selecionar "Name (Z to A)"<br>2. Verificar a ordem<br>3. Selecionar "Name (A to Z)" | Lista reordenada alfabeticamente nos dois sentidos | Média | A executar |
| CT-012 | Ordenar por preço (menor e maior) | Logado | 1. Selecionar "Price (low to high)"<br>2. Verificar a ordem<br>3. Selecionar "Price (high to low)" | Lista começa em $7.99 no primeiro caso e em $49.99 no segundo | Média | A executar |
| CT-013 | Página de detalhe do produto | Logado | 1. Clicar no nome "Sauce Labs Backpack" | Página de detalhe mostra o mesmo nome, descrição e preço da listagem ($29.99) | Média | A executar |
| CT-014 | Voltar da página de detalhe | Na página de detalhe de um produto | 1. Clicar em "Back to products" | Usuário volta para a listagem | Baixa | A executar |

## Carrinho

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Prioridade | Status |
|---|---|---|---|---|---|---|
| CT-015 | Adicionar um produto | Logado, carrinho vazio | 1. Clicar em "Add to cart" no "Sauce Labs Backpack" | Botão muda para "Remove" e o ícone do carrinho mostra 1 | Alta | Passou ([evidência](../evidencias/CT-015-adicionar-produto.png)) |
| CT-016 | Adicionar todos os produtos | Logado, carrinho vazio | 1. Clicar em "Add to cart" nos 6 produtos<br>2. Repetir com `problem_user` | Ícone mostra 6 e todos aparecem no carrinho | Alta | A executar |
| CT-017 | Remover produto pela listagem | 1 produto no carrinho | 1. Clicar em "Remove" na listagem | Botão volta para "Add to cart" e o contador some | Média | A executar |
| CT-018 | Remover produto dentro do carrinho | 2 produtos no carrinho | 1. Abrir o carrinho<br>2. Clicar em "Remove" em um item | Item sai da lista e o contador mostra 1 | Média | A executar |
| CT-019 | Carrinho mantido após navegar | 2 produtos no carrinho | 1. Abrir o detalhe de um produto<br>2. Voltar para a listagem<br>3. Abrir o carrinho | Os 2 produtos continuam no carrinho | Média | A executar |

## Checkout

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Prioridade | Status |
|---|---|---|---|---|---|---|
| CT-020 | Compra completa com dados válidos | "Sauce Labs Backpack" e "Sauce Labs Bike Light" no carrinho | 1. Abrir o carrinho e clicar em Checkout<br>2. Preencher `Maria`, `Souza`, `15775000`<br>3. Clicar em Continue<br>4. Clicar em Finish | Mensagem "Thank you for your order!" e carrinho esvaziado | Alta | Passou ([evidência](../evidencias/CT-020-compra-concluida.png)) |
| CT-021 | Cálculo do resumo do pedido | Mesmos itens do CT-020, na tela de resumo | 1. Conferir os valores exibidos | Item total $39.98, imposto (Tax) $3.20 (8%) e total $43.18 | Alta | Passou ([evidência](../evidencias/CT-021-resumo-do-pedido.png)) |
| CT-022 | Campo nome obrigatório | Na tela de dados do checkout | 1. Deixar o nome vazio e preencher os outros campos<br>2. Clicar em Continue | Mensagem "First Name is required" | Média | A executar |
| CT-023 | Campo sobrenome obrigatório | Na tela de dados do checkout | 1. Deixar o sobrenome vazio e preencher os outros campos<br>2. Clicar em Continue | Mensagem "Last Name is required" | Média | A executar |
| CT-024 | Campo CEP obrigatório | Na tela de dados do checkout | 1. Deixar o CEP vazio e preencher os outros campos<br>2. Clicar em Continue | Mensagem "Postal Code is required" | Média | A executar |
| CT-025 | Checkout com carrinho vazio | Logado, carrinho vazio | 1. Abrir o carrinho<br>2. Clicar em Checkout | Sistema impede o checkout ou informa que o carrinho está vazio | Alta | A executar |
| CT-026 | Cancelar o checkout | Na tela de resumo do pedido | 1. Clicar em Cancel | Usuário volta para a listagem e os itens continuam no carrinho | Média | A executar |

## Menu e sessão

| ID | Cenário | Pré-condição | Passos | Resultado esperado | Prioridade | Status |
|---|---|---|---|---|---|---|
| CT-027 | Logout | Logado | 1. Abrir o menu lateral<br>2. Clicar em Logout | Usuário volta para a tela de login | Alta | Passou ([evidência](../evidencias/CT-027-logout.png)) |
| CT-028 | Voltar no navegador após logout | Ter feito logout | 1. Clicar no botão voltar do navegador | Página de produtos não é exibida e o usuário continua na tela de login | Média | A executar |

## Registro de execução

| Data | Etapa | Casos | Resultado |
|---|---|---|---|
| 30/10/2026 | 1. Smoke test (`standard_user`) | CT-001, CT-009, CT-015, CT-020, CT-021, CT-027 | 6 passaram, 0 falharam |
| 03/11/2026 | 2. Login (`standard_user`, `locked_out_user` e usuário inexistente) | CT-002 a CT-007 | 6 passaram, 0 falharam |

## Rastreabilidade com os bugs

| Caso | Bug |
|---|---|
| CT-002, CT-003, CT-007 | [BUG-007](../bugs/BUG-007-mensagem-de-erro-vaza-da-caixa.md) |
