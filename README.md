# Testes manuais — SauceDemo (Swag Labs)

![Status](https://img.shields.io/badge/status-em%20execu%C3%A7%C3%A3o-yellow) ![Tipo](https://img.shields.io/badge/testes-manuais-blue) ![Casos](https://img.shields.io/badge/casos%20de%20teste-28-informational)

Projeto de testes manuais da loja de demonstração [SauceDemo](https://www.saucedemo.com), cobrindo o fluxo principal de compra: login, listagem de produtos, carrinho e checkout.

O objetivo é trabalhar como num projeto real: entender a aplicação, planejar o que testar e por quê, escrever casos de teste rastreáveis, executar e documentar os defeitos de forma que um desenvolvedor consiga reproduzir sem precisar me perguntar nada.

> **Status:** planejamento concluído, execução em andamento. Os documentos são publicados conforme cada etapa é concluída.

## Documentação

| Documento | Conteúdo | Situação |
|---|---|---|
| [Plano de testes](docs/plano-de-testes.md) | Escopo, estratégia, ordem de execução, riscos e critérios de entrada e saída | Publicado |
| Casos de teste | 28 casos organizados em 5 módulos, com prioridade e status de execução | Em breve |
| Relatórios de bug | Defeitos com passos, evidência, severidade e prioridade ([modelo](bugs/TEMPLATE.md)) | Durante a execução |
| Relatório de execução | Resultado da rodada de testes e conclusão | Ao final |

## Cobertura planejada

| Módulo | Casos |
|---|---|
| Login | 8 |
| Produtos | 6 |
| Carrinho | 5 |
| Checkout | 7 |
| Menu e sessão | 2 |
| **Total** | **28** |

## Abordagem

- **Técnicas:** partição de equivalência e análise de valor limite nos formulários, teste baseado em fluxo para o processo de compra e testes exploratórios com sessões de tempo definido.
- **Usuários de teste:** a aplicação oferece perfis com comportamentos diferentes. O `standard_user` é a referência, e os mesmos cenários são comparados com `problem_user`, `locked_out_user` e `performance_glitch_user` para isolar falhas.
- **Priorização:** os casos de prioridade alta cobrem o caminho que gera receita (login → carrinho → compra concluída) e são executados primeiro, num smoke test.

## Ambiente

- Aplicação: https://www.saucedemo.com
- Navegador: Google Chrome (versão registrada no relatório de execução)
- Sistema operacional: Windows 11
- Resolução: 1920x1080

## Próximos passos

- Automatizar os casos de prioridade alta com Cypress (repositório separado).
- Adicionar testes de responsividade em resolução mobile.

---

Abner Davi · [LinkedIn](https://www.linkedin.com/in/abner-davi-qa) · abnerdavi.dev@gmail.com
