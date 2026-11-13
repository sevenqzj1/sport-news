# Testes e qualidade

## 1. Situação atual

Não foram encontrados arquivos de teste, diretório de testes, scripts de teste ou configuração de framework de testes no pacote analisado. Assim, não há cobertura automatizada comprovada.

## 2. Estratégia recomendada

A qualidade deve ser verificada em quatro níveis:

| Nível | Objetivo | Exemplos |
|---|---|---|
| Unitário | Validar funções isoladas | Normalização de texto, filtros, validação de campos |
| Integração | Validar componentes juntos | Rotas com repositório MySQL e serviços externos simulados |
| Contrato | Garantir compatibilidade cliente/API | Formatos de notícias, resultados e preferências |
| Ponta a ponta | Validar jornadas reais | Página, filtros, preferências e falhas de rede |

## 3. Casos de teste do frontend

### Notícias

- resposta como array;
- resposta como objeto com `noticias`;
- resposta como objeto com `data`;
- resposta vazia;
- HTTP não sucedido;
- JSON inválido;
- notícia sem título, fonte ou URL;
- URL com protocolo não permitido.

### Resultados

- resposta válida com partidas agendadas;
- partidas ao vivo e finalizadas;
- placar nulo;
- dados opcionais de intervalo e agregado;
- campeonato sem resultados;
- filtro Todos;
- filtro por cada liga;
- erro de rede e retorno vazio.

### Preferências

- resposta direta;
- resposta aninhada em `preferencias`;
- nomes em camelCase e snake_case;
- formulário incompleto;
- resposta de gravação bem-sucedida;
- falha HTTP ao salvar;
- falha de rede.

## 4. Casos de teste do backend a implementar

- inicialização com variáveis ausentes;
- conexão MySQL indisponível;
- consulta parametrizada;
- payload malformado;
- limite de campos e tamanho de conteúdo;
- falha na API externa;
- timeout e limite de uso da API externa;
- CORS para origem autorizada e não autorizada;
- resposta de erro sem detalhes internos.

## 5. Critérios mínimos para release

- todas as rotas documentadas cobertas por testes de contrato;
- nenhuma credencial incluída no repositório;
- instalação reproduzível a partir do manifesto e lockfile;
- schema aplicado em banco limpo;
- frontend sem erros críticos no console;
- atualizações automáticas não criam requisições concorrentes descontroladas;
- instruções de deploy verificadas em ambiente limpo.

## 6. Evidências

Ao adicionar a suíte, documente no repositório:

- comando exato para executar os testes;
- versão do runtime;
- serviços necessários;
- variáveis de ambiente de teste;
- resultado do último pipeline.

Até que isso exista, o estado da suíte deve permanecer como **não configurada / não verificada**.
