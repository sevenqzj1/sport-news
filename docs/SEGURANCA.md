# Segurança

## 1. Aviso prioritário sobre credenciais

O arquivo ZIP versionado contém uma entrada chamada `backend/.env`. O arquivo `LEIA-ANTES.txt` afirma que o ambiente real não deveria ser incluído e orienta a gerar nova chave e trocar a senha caso credenciais anteriores sejam reais.

O conteúdo do arquivo não é reproduzido nesta documentação. Como o pacote está armazenado no GitHub, trate qualquer segredo que tenha sido colocado nele como potencialmente exposto.

Ações imediatas:

1. Revogue e gere novamente a chave OpenFoot, se ela for real.
2. Altere a senha do MySQL e qualquer outra credencial que tenha sido incluída.
3. Remova o arquivo `.env` do ZIP e de futuras versões.
4. Verifique o histórico de commits e considere reescrever o histórico para remover o segredo.
5. Armazene os novos valores somente em Secrets ou variáveis privadas do provedor.

Remover o arquivo apenas em um commit novo não elimina cópias que permaneceram no histórico.

## 2. Variáveis de ambiente

O arquivo `.env.example` contém placeholders. Ele deve ser a referência versionada para a configuração local.

Regras:

- `.env` deve permanecer fora do Git;
- segredos não podem ser enviados ao navegador;
- não registrar tokens e senhas em logs;
- separar credenciais de desenvolvimento e produção;
- usar rotação de credenciais e privilégios mínimos.

## 3. Banco de dados

O conector usa MySQL e recebe host, usuário, senha e nome de banco por variáveis de ambiente.

Antes de produção:

- criar um usuário de banco específico para a aplicação;
- conceder somente os privilégios necessários;
- parametrizar toda consulta que receba dados externos;
- configurar TLS conforme exigência do provedor;
- evitar mensagens de erro SQL detalhadas na resposta HTTP;
- limitar conexões e tempos de espera.

A presença do pacote `mysql2` não comprova que as consultas do backend estejam implementadas ou protegidas.

## 4. API e validação

Os handlers da API não foram localizados no ZIP. A implementação deverá contemplar:

- validação de tipos, comprimentos e campos obrigatórios;
- tratamento de payloads inválidos;
- limites de requisições e proteção contra abuso;
- política CORS restrita aos domínios autorizados;
- respostas de erro padronizadas;
- logs sem dados sensíveis;
- autenticação e autorização, caso sejam introduzidas contas e preferências privadas.

Não exponha uma rota de atualização de preferências sem definir quem pode alterar os dados.

## 5. Frontend

O JavaScript possui uma função `escaparHTML` para codificar texto inserido em elementos HTML. Essa proteção deve ser mantida e coberta por testes.

Também é necessário validar o esquema e o destino de URLs recebidas da API antes de utilizá-las em atributos `href` ou `src`. A codificação HTML, isoladamente, não substitui uma allowlist de protocolos e domínios.

Links abertos em nova aba devem manter proteção contra acesso à janela de origem.

## 6. Dependências

O ZIP contém `node_modules` e um lockfile interno, mas não contém `package.json`. Isso dificulta auditoria reproduzível e atualização controlada.

Recomendações:

- versionar o manifesto e o lockfile oficial;
- não versionar `node_modules`;
- executar auditoria de dependências no pipeline;
- atualizar dependências de forma controlada;
- revisar especialmente bibliotecas que processam tokens, dados externos e conexões SQL.

## 7. Checklist de segurança

- [ ] Segredos revogados e rotacionados.
- [ ] Arquivo `.env` removido do pacote e do histórico, quando necessário.
- [ ] `.gitignore` validado para ignorar arquivos de ambiente.
- [ ] Secrets configurados na hospedagem.
- [ ] Consultas parametrizadas.
- [ ] CORS restrito.
- [ ] Validação de dados e URLs.
- [ ] Rate limiting e tratamento de erros.
- [ ] TLS habilitado.
- [ ] Auditoria de dependências automatizada.
