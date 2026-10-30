# Plano de testes — SauceDemo

| Item | Detalhe |
|---|---|
| Projeto | SauceDemo (Swag Labs) |
| Versão do documento | 1.0 |
| Responsável | Abner Davi |
| Data | 29/10/2026 |

## 1. Objetivo

Verificar se um usuário consegue entrar na loja, escolher produtos e concluir uma compra com os valores corretos, e identificar falhas que impeçam ou prejudiquem esse fluxo.

## 2. Escopo

### Dentro do escopo

| Módulo | O que é verificado |
|---|---|
| Login | Autenticação válida e inválida, mensagens de erro, usuário bloqueado, acesso direto a páginas sem login |
| Produtos | Listagem, dados dos produtos, ordenação, página de detalhe |
| Carrinho | Adicionar, remover, contador do ícone, persistência entre páginas |
| Checkout | Validação dos campos, resumo do pedido, cálculo de imposto e total, conclusão e cancelamento |
| Menu e sessão | Logout e bloqueio de acesso após sair |

### Fora do escopo

- Testes de carga e desempenho com medição formal
- Testes de segurança (injeção, força bruta)
- Pagamento real: a aplicação não processa pagamento
- Navegadores além do Chrome nesta rodada
- Links externos do rodapé (redes sociais)

## 3. Estratégia

**Tipos de teste:** funcional, de interface e exploratório.

**Técnicas:**
- Partição de equivalência e valor limite nos campos de login e checkout (vazio, válido, formato inválido).
- Teste baseado em fluxo para o caminho completo de compra.
- Teste exploratório em sessões de 30 minutos, com foco em carrinho e checkout, registrando o que foi explorado e o que foi encontrado.
- Comparação entre perfis de usuário: o mesmo cenário é executado no `standard_user` e no `problem_user` para confirmar se a falha é do perfil ou da aplicação.

**Priorização:**

| Prioridade | Critério |
|---|---|
| Alta | Impede o usuário de comprar ou gera valor errado |
| Média | Atrapalha o uso, mas existe alternativa |
| Baixa | Problema visual ou de texto sem impacto no fluxo |

## 4. Ambiente e dados de teste

- URL: https://www.saucedemo.com
- Navegador: Google Chrome (versão registrada no relatório de execução), janela 1920x1080
- Sistema operacional: Windows 11
- Senha de todos os usuários: `secret_sauce`

| Usuário | Uso nos testes |
|---|---|
| `standard_user` | Referência de comportamento esperado |
| `locked_out_user` | Validação de usuário bloqueado |
| `problem_user` | Perfil com falhas simuladas na interface |
| `performance_glitch_user` | Perfil com lentidão simulada no login |

Dados para o checkout: nome `Maria`, sobrenome `Souza`, CEP `15775000`.

## 5. Ordem de execução

A execução começa pelo fluxo principal. Se ele falhar, não faz sentido seguir para os detalhes.

| Etapa | Usuário | Casos | Objetivo |
|---|---|---|---|
| 1. Smoke test | `standard_user` | CT-001, CT-009, CT-015, CT-020, CT-021, CT-027 | Confirmar que a compra completa funciona. Se algum falhar, registrar o bug e avaliar se vale continuar |
| 2. Login | `standard_user` e outros indicados | CT-002 a CT-007 | Validar erros e bloqueios de acesso |
| 3. Produtos | `standard_user` | CT-011 a CT-014 | Ordenação e página de detalhe |
| 4. Carrinho | `standard_user` | CT-016 a CT-019 | Adicionar, remover e manter itens |
| 5. Checkout | `standard_user` | CT-022 a CT-026 | Validações, carrinho vazio e cancelamento |
| 6. Sessão | `standard_user` | CT-028 | Acesso após logout |
| 7. Comparação de perfis | `problem_user` | CT-010, CT-011, CT-012, CT-016, CT-023 | Repetir os cenários e comparar com o `standard_user` |
| 8. Desempenho | `performance_glitch_user` | CT-008 | Medir o tempo de login |
| 9. Sessão exploratória | `standard_user` | Checkout, 30 minutos | Procurar entradas que o sistema deveria recusar |
| 10. Fechamento | — | — | Revisar os bugs, conferir as evidências e preencher o relatório de execução |

Durante a execução:
- Antes de cada caso, fazer logout e login novamente para começar de um estado limpo.
- Ao encontrar uma falha, tirar o print na hora e anotar o ID do caso. O relatório de bug pode ser escrito no fim da etapa.
- Atualizar o status na tabela de casos assim que terminar cada um.

## 6. Critérios de entrada

- Aplicação acessível no endereço acima.
- Casos de teste revisados.
- Usuários de teste funcionando.

## 7. Critérios de saída

- 100% dos casos de prioridade alta executados.
- Todos os defeitos encontrados registrados com evidência.
- Nenhum defeito crítico em aberto sem registro no relatório de execução.

## 8. Riscos

| Risco | Impacto | Como tratar |
|---|---|---|
| A aplicação é pública e pode mudar sem aviso | Resultados deixam de ser reproduzíveis | Registrar data e versão do navegador em cada execução e guardar evidências |
| Alguns perfis têm falhas propositais | Confundir comportamento do perfil com defeito da aplicação | Sempre repetir o cenário no `standard_user` antes de concluir |
| Sessão expira após cerca de 10 minutos | Falso negativo durante a execução | Refazer o login no início de cada caso |

## 9. Entregáveis

- Plano de testes (este documento)
- [Casos de teste](casos-de-teste.md)
- [Relatórios de bug](../bugs/)
- [Relatório de execução](relatorio-de-execucao.md)

## 10. Severidade dos defeitos

| Severidade | Definição |
|---|---|
| Crítica | Bloqueia uma função principal sem alternativa (ex.: não é possível comprar) |
| Alta | Função principal com resultado errado ou funcionando só em parte |
| Média | Função secundária com falha, ou falha principal com alternativa |
| Baixa | Problema cosmético ou de texto |
