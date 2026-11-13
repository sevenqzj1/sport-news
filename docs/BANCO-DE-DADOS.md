# Banco de dados

## 1. Tecnologia identificada

O arquivo `backend/database.js` utiliza o pacote `mysql2` e cria uma conexão com MySQL. O nome de banco padrão configurado no código é `sportnews`, e o charset utilizado é `utf8mb4`.

## 2. Configuração observada

| Variável | Comportamento no código |
|---|---|
| `DB_HOST` | Host; padrão `localhost` |
| `DB_USER` | Usuário; padrão `root` |
| `DB_PASSWORD` | Senha; sem valor padrão explícito |
| `DB_NAME` | Banco; padrão `sportnews` |

O código carrega as variáveis do arquivo `.env` localizado na pasta `backend`, por meio de `dotenv`.

Não foi observado uso explícito de `DB_PORT`, configuração de SSL, pool de conexões ou timeout customizado no arquivo analisado.

## 3. Comportamento do conector

O módulo:

1. carrega as variáveis de ambiente;
2. instancia `mysql.createConnection(...)`;
3. tenta abrir a conexão;
4. escreve uma mensagem no console em caso de sucesso ou falha;
5. exporta o objeto de conexão.

É uma conexão única, não um pool. A implementação de rotas, consultas e transações não foi localizada no pacote.

## 4. Schema e migrations

**Não foi encontrado arquivo SQL de criação do banco, migration ou definição verificável de tabelas.** Por isso, não é correto afirmar quais tabelas existem, quais campos são persistidos ou quais relacionamentos foram implementados.

O nome `sportnews` é o valor padrão usado pelo conector; isso não cria o banco automaticamente.

## 5. Preparação do banco

Depois de recuperar o schema oficial, crie o banco com charset compatível. Exemplo de criação do banco vazio:

```sql
CREATE DATABASE sportnews
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;
```

Esse comando cria somente o banco. Ele **não** cria tabelas e não torna as rotas da API funcionais.

Não execute scripts encontrados em fontes não verificadas em produção. O schema deve ser versionado no repositório, revisado e testado antes do deploy.

## 6. Modelo lógico a definir

Com base nos recursos da interface, o modelo de persistência ainda precisa ser especificado. Uma futura modelagem pode considerar:

- preferências de times e jogador;
- cache de notícias e metadados da fonte;
- partidas, campeonato, equipes, horários e placares;
- histórico de atualização e origem dos dados.

A lista é uma proposta de domínio. Não representa tabelas atualmente confirmadas.

## 7. Recomendações técnicas

- Adotar pool de conexões para aplicações com múltiplas requisições simultâneas.
- Utilizar consultas parametrizadas.
- Criar usuário de banco com privilégios mínimos; evitar `root` fora do ambiente local.
- Adicionar migrations versionadas e um procedimento de rollback.
- Documentar índices, chaves únicas e política de retenção.
- Configurar TLS quando exigido pelo provedor do MySQL.
- Não registrar senhas, tokens ou dados sensíveis nos logs.
- Testar conectividade e falhas de banco durante a inicialização.

## 8. Pendências

- [ ] Recuperar e versionar o schema MySQL.
- [ ] Identificar as tabelas realmente usadas pelos handlers da API.
- [ ] Definir a política de armazenamento das preferências.
- [ ] Implementar migrations.
- [ ] Definir pool, timeout, SSL e tratamento de reconexão.
- [ ] Adicionar testes de integração do repositório de dados.
