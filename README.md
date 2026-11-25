# Testes manuais — SauceDemo (Swag Labs)

![Status](https://img.shields.io/badge/status-conclu%C3%ADdo-brightgreen) ![Tipo](https://img.shields.io/badge/testes-manuais-blue) ![Casos](https://img.shields.io/badge/casos%20de%20teste-28-informational) ![Bugs](https://img.shields.io/badge/bugs%20registrados-12-red)

Projeto de testes manuais da loja de demonstração [SauceDemo](https://www.saucedemo.com), cobrindo o fluxo principal de compra: login, listagem de produtos, carrinho e checkout.

O objetivo é trabalhar como num projeto real: entender a aplicação, planejar o que testar e por quê, escrever casos de teste rastreáveis, executar e documentar os defeitos de forma que um desenvolvedor consiga reproduzir sem precisar me perguntar nada.

> **Status:** rodada 1 concluída (30/10/2026 a 24/11/2026). 28 casos executados, 21 passaram, 7 falharam e 12 defeitos foram registrados.

## Documentação

| Documento | Conteúdo |
|---|---|
| [Plano de testes](docs/plano-de-testes.md) | Escopo, estratégia, ordem de execução, riscos e critérios de entrada e saída |
| [Casos de teste](docs/casos-de-teste.md) | 28 casos em 5 módulos, com prioridade, status, evidência e rastreabilidade com os bugs |
| [Relatórios de bug](bugs/README.md) | 12 defeitos com passos, resultado esperado e atual, impacto, severidade, prioridade e evidência ([modelo](bugs/TEMPLATE.md)) |
| [Relatório de execução](docs/relatorio-de-execucao.md) | Resultado por módulo, ambiente, sessão exploratória, critérios de saída e conclusão |
| [Evidências](evidencias/) | Prints de cada caso executado e de cada defeito |

## Resultado

| Módulo | Casos | Passou | Falhou |
|---|---|---|---|
| Login | 8 | 7 | 1 |
| Produtos | 6 | 3 | 3 |
| Carrinho | 5 | 4 | 1 |
| Checkout | 7 | 5 | 2 |
| Menu e sessão | 2 | 2 | 0 |
| **Total** | **28** | **21** | **7** |

Defeitos por severidade: 1 crítico, 4 altos, 6 médios e 1 baixo.

## Destaques

- **[BUG-001](bugs/BUG-001-checkout-carrinho-vazio.md): compra concluída com o carrinho vazio.** O botão Checkout continua habilitado sem itens, e o pedido chega à confirmação com total de $0.00.
- **[BUG-012](bugs/BUG-012-checkout-pula-dados-pela-url.md): pedido sem os dados do comprador.** Abrindo o resumo do checkout direto pela URL, a etapa de nome e CEP é pulada e o pedido é finalizado. Encontrado na sessão exploratória.
- **[BUG-011](bugs/BUG-011-carrinho-compartilhado-entre-usuarios.md): carrinho passa de um usuário para outro.** O carrinho fica salvo no navegador e aparece para o próximo usuário que entrar.
- **[BUG-009](bugs/BUG-009-enter-no-checkout-aciona-cancel.md): Enter no checkout cancela a compra.** A causa está no HTML: o botão Cancel não tem `type="button"` e vem antes do Continue no formulário.
- **[BUG-003](bugs/BUG-003-sobrenome-nao-aceita-digitacao.md): compra bloqueada para o `problem_user`.** O que é digitado no sobrenome substitui o nome, e a validação impede o avanço.

## Abordagem

- **Técnicas:** partição de equivalência e análise de valor limite nos formulários, teste baseado em fluxo para o processo de compra e teste exploratório com missão definida.
- **Usuários de teste:** o `standard_user` é a referência, e os mesmos cenários são comparados com `problem_user`, `locked_out_user` e `performance_glitch_user` para separar falhas do perfil de falhas da aplicação.
- **Priorização:** os casos de prioridade alta cobrem o caminho que gera receita (login → carrinho → compra concluída) e foram executados primeiro, num smoke test.

## Ambiente

- Aplicação: https://www.saucedemo.com
- Navegadores baseados em Chromium: Chromium 152 (etapas 1 a 4) e Brave 158 (etapas 5 a 9)
- Sistema operacional: Windows
- Detalhes de versão e janela por etapa no [relatório de execução](docs/relatorio-de-execucao.md#ambiente)

## Próximos passos

- Automatizar os casos de prioridade alta com Cypress (repositório separado).
- Reexecutar os casos de carrinho e checkout depois da correção dos bugs de prioridade alta.
- Adicionar testes de responsividade em resolução mobile.

---

Abner Davi · [LinkedIn](https://www.linkedin.com/in/abner-davi-qa) · abnerdavi.dev@gmail.com
