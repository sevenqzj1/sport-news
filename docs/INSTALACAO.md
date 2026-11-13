# Instalação e execução

## 1. Estado do pacote

O conteúdo da aplicação está dentro de `backend.zip`. O arquivo contém o frontend, `database.js`, `.env.example`, um lockfile interno de dependências e uma pasta `node_modules`.

O pacote examinado não contém:

- `package.json`;
- ponto de entrada identificável do servidor;
- implementação das rotas `/api`;
- schema SQL ou migrations;
- configuração de deploy verificável.

O arquivo `LEIA-ANTES.txt` recomenda `npm install` e `npm start`, mas esses comandos não podem ser garantidos sem o manifesto e o código do servidor.

## 2. Pré-requisitos previstos

Para completar a aplicação, o ambiente deverá possuir:

- Node.js em versão LTS compatível com as dependências recuperadas;
- npm;
- servidor MySQL;
- credenciais válidas de banco;
- chave OpenFoot, caso a integração seja realmente utilizada.

A versão exata do Node.js e os scripts npm ainda precisam ser definidos no `package.json` do projeto.

## 3. Preparar as variáveis de ambiente

Depois de extrair o ZIP, acesse a pasta `backend` e copie o arquivo de exemplo:

Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Linux/macOS:

```bash
cp .env.example .env
```

Edite o arquivo `.env` localmente:

```dotenv
OPENFOOT_API_KEY=INSIRA_UMA_CHAVE_NOVA
OPENFOOT_EVENTS_ENABLED=false

DB_HOST=localhost
DB_USER=usuario_local
DB_PASSWORD=senha_local
DB_NAME=sportnews
```

Os valores acima são placeholders. Não reutilize nenhuma chave ou senha que possa ter aparecido em um pacote anterior.

## 4. Preparar o MySQL

Crie o banco vazio:

```sql
CREATE DATABASE sportnews
  CHARACTER SET utf8mb4
  COLLATE utf8mb4_unicode_ci;
```

Esse passo não cria as tabelas. O schema oficial não foi encontrado no pacote. A aplicação completa depende da recuperação desse schema e das rotas que executam as consultas.

## 5. Visualizar apenas o frontend

Para uma prévia visual sem backend, é possível servir a pasta `frontend` com Python:

```bash
python -m http.server 5500 --directory frontend
```

Depois, abra `http://localhost:5500`.

Essa prévia serve somente arquivos estáticos. As chamadas do frontend para `/api/noticias-auto`, `/api/resultados` e `/api/preferencias` não serão atendidas por esse servidor simples e deverão falhar até que a API exista.

## 6. Como habilitar a execução completa

Antes de usar `npm install` e `npm start`, recupere ou crie:

1. `package.json` com dependências diretas e scripts documentados;
2. ponto de entrada do servidor;
3. rotas e controladores correspondentes ao [contrato da API](API.md);
4. inicialização e encerramento controlados da conexão MySQL;
5. schema e migrations do banco;
6. testes de inicialização, persistência e integração com a fonte externa.

Não é seguro inventar um comando de start sem saber qual arquivo deve iniciar o servidor.

## 7. Implantação

Ainda não foi encontrado Dockerfile, workflow de CI/CD ou configuração de hospedagem para este repositório.

Quando o backend estiver completo, a implantação deverá configurar os Secrets no ambiente de hospedagem, executar migrations controladas, expor apenas a porta necessária e fornecer HTTPS. Nunca inclua `.env` ou credenciais na imagem, no frontend ou nos logs.

## 8. Checklist de validação

- [ ] O servidor inicia sem erros.
- [ ] O MySQL está acessível e o schema foi aplicado.
- [ ] `GET /api/noticias-auto` retorna JSON válido.
- [ ] `GET /api/resultados` retorna JSON válido.
- [ ] `GET /api/preferencias` retorna o formato documentado.
- [ ] `POST /api/preferencias` persiste os dados.
- [ ] A integração externa responde ou apresenta erro controlado.
- [ ] As variáveis privadas estão configuradas no ambiente.
- [ ] A aplicação funciona por HTTPS.
