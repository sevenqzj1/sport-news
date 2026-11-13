# Status técnico e roadmap

## 1. Resumo executivo

O repositório contém uma interface de portal de futebol e um pacote ZIP com um conector MySQL e dependências Node. O frontend descreve um fluxo de notícias, resultados e preferências, mas o backend que deveria fornecer esses dados não foi localizado no pacote.

O estado atual deve ser considerado **protótipo/frontend em desenvolvimento**, não uma aplicação full-stack comprovadamente pronta para produção.

## 2. Matriz de implementação

| Componente | Estado observado | Próxima ação |
|---|---|---|
| Página principal | Presente | Extrair para estrutura normal |
| Estilos | Presente | Revisar responsividade e acessibilidade |
| Lógica de notícias | Presente no cliente | Integrar com endpoint real |
| Lógica de resultados | Presente no cliente | Integrar com endpoint real |
| Filtros de campeonato | Presente no cliente | Adicionar testes |
| Modal e formulário de preferências | Presente no cliente | Integrar com persistência |
| Conector MySQL | Presente | Evoluir para pool e tratamento de falhas |
| Servidor Node.js | Não localizado | Recuperar ou implementar |
| Rotas HTTP | Não localizadas | Implementar conforme `API.md` |
| Manifesto npm | Não localizado | Criar e fixar dependências diretas |
| Schema SQL | Não localizado | Recuperar e versionar migrations |
| Integração OpenFoot | Variáveis de ambiente presentes; consumidor não localizado | Recuperar implementação e documentar limites |
| Testes automatizados | Não localizados | Criar suíte e pipeline |
| Deploy | Não localizado | Documentar ambiente e Secrets |
| Segurança de credenciais | ZIP contém `.env` | Rotacionar segredos e remover o arquivo |

## 3. Prioridade crítica — antes de qualquer deploy

1. Rotacionar credenciais que possam ter sido incluídas em `.env`.
2. Remover o arquivo de ambiente do pacote e revisar o histórico do Git.
3. Recuperar ou implementar o servidor e as rotas.
4. Restaurar `package.json` e lockfile reproduzível.
5. Recuperar e versionar o schema SQL.
6. Executar testes de integração com banco e APIs externas.

## 4. Prioridade alta — robustez

- criar uma camada de serviços para notícias e partidas;
- aplicar cache e controle de frequência na fonte externa;
- padronizar mensagens e códigos de erro da API;
- configurar validação de payloads;
- implementar pool de conexões MySQL;
- definir autenticação antes de associar preferências a pessoas;
- adicionar testes de contrato e pipeline de CI.

## 5. Evolução futura

- filtros adicionais por time, competição e período;
- busca de notícias;
- paginação;
- histórico de partidas;
- favoritos persistidos por conta;
- observabilidade, logs estruturados e métricas;
- cache com invalidação controlada.

Esses itens são possibilidades de evolução, não funcionalidades confirmadas.

## 6. Critério de conclusão

O projeto poderá ser considerado pronto para uma primeira versão quando:

- a instalação funcionar em ambiente limpo;
- servidor e endpoints estiverem versionados;
- banco puder ser criado por migrations;
- integração externa tiver limites e erros documentados;
- credenciais estiverem fora do Git;
- testes automatizados essenciais passarem;
- deploy e rollback estiverem documentados e validados.
