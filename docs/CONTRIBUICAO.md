# Guia de contribuição

## 1. Objetivo

Este guia define um fluxo de trabalho previsível para corrigir bugs, implementar funcionalidades e revisar alterações no SPORTNEWS.

## 2. Preparação do ambiente

Antes de iniciar uma alteração:

1. clone o repositório;
2. leia o README e os documentos em `docs/`;
3. não reutilize o arquivo `.env` do ZIP;
4. configure credenciais locais próprias;
5. confirme que a instalação e os testes estão disponíveis.

No estado atual, o backend não pode ser inicializado de forma reproduzível porque faltam o manifesto npm e o servidor. Trabalhos que dependam dele devem começar pela recuperação desses arquivos.

## 3. Branches

Utilize branches descritivas:

| Tipo | Exemplo |
|---|---|
| Funcionalidade | `feat/filtro-por-campeonato` |
| Correção | `fix/erro-carregamento-noticias` |
| Documentação | `docs/atualiza-arquitetura` |
| Segurança | `security/remove-secrets` |
| Refatoração | `refactor/separa-servicos-api` |

Evite desenvolver diretamente na branch principal.

## 4. Commits

Prefira mensagens curtas no padrão Conventional Commits:

- `feat: adiciona filtro de campeonato`
- `fix: trata falha ao carregar resultados`
- `docs: documenta contrato de preferencias`
- `refactor: separa acesso ao banco`
- `test: adiciona testes das rotas`
- `security: remove arquivo de ambiente`

## 5. Pull requests

Toda contribuição deve incluir:

- objetivo e contexto;
- arquivos alterados;
- comportamento anterior e novo;
- evidência visual quando alterar a interface;
- testes executados e resultado;
- variáveis ou migrations necessárias;
- riscos, limitações e plano de rollback.

## 6. Padrões de implementação

- manter a interface acessível e responsiva;
- preservar a compatibilidade com o contrato documentado da API;
- validar e normalizar dados no servidor;
- usar consultas SQL parametrizadas;
- nunca commitar credenciais;
- manter documentação e exemplos alinhados ao código;
- não adicionar `node_modules` ao repositório;
- evitar dependências sem justificativa técnica.

## 7. Checklist de revisão

- [ ] A alteração resolve o problema descrito.
- [ ] O código não contém segredos ou dados privados.
- [ ] Entradas externas são validadas.
- [ ] Erros são tratados e apresentados adequadamente.
- [ ] Testes relevantes foram executados.
- [ ] Documentação foi atualizada.
- [ ] Migrations e variáveis novas estão descritas.
- [ ] O pull request não inclui arquivos gerados desnecessários.
