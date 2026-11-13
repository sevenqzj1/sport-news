# Contrato da API

## 1. Escopo

Este documento formaliza o contrato que o frontend do SPORTNEWS espera consumir. As rotas foram identificadas em `frontend/js/main.js`.

> **Importante:** os handlers do backend não foram encontrados no ZIP analisado. Portanto, os exemplos abaixo são formatos compatíveis com o cliente e uma especificação para implementação, não evidência de endpoints já operacionais.

Prefixo usado pelo frontend: `/api`.

## 2. Endpoints

| Método | Endpoint | Uso no frontend |
|---|---|---|
| GET | `/api/noticias-auto` | Carregar notícias |
| GET | `/api/resultados` | Carregar jogos e placares |
| GET | `/api/preferencias` | Recuperar preferências |
| POST | `/api/preferencias` | Salvar preferências |

## 3. GET /api/noticias-auto

Retorna uma lista de notícias. O cliente aceita um array diretamente ou um objeto contendo `noticias` ou `data`.

Exemplo compatível:

```json
[
  {
    "titulo": "Título da notícia",
    "descricao": "Resumo da notícia",
    "fonte": "Nome da fonte",
    "categoria": "Brasileirão",
    "url": "https://exemplo.com/noticia"
  }
]
```

Aliases aceitos pelo frontend:

| Campo preferencial | Alias também aceito |
|---|---|
| `titulo` | `title` |
| `descricao` | `description` |
| `fonte` | `source` |
| `categoria` | `modalidade` |
| `url` | `link` |

O frontend exibe no máximo 12 notícias por atualização.

## 4. GET /api/resultados

Retorna uma lista de partidas. O cliente aceita um array diretamente ou um objeto contendo `resultados` ou `data`.

Exemplo compatível:

```json
[
  {
    "equipe_casa": "Equipe A",
    "equipe_fora": "Equipe B",
    "campeonato": "Brasileirão Série A",
    "fase": "Rodada",
    "horario": "20:00",
    "status": "Agendado",
    "placar_casa": null,
    "placar_fora": null,
    "escudo_casa": "https://exemplo.com/equipe-a.png",
    "escudo_fora": "https://exemplo.com/equipe-b.png",
    "placar_intervalo_casa": null,
    "placar_intervalo_fora": null,
    "placar_agregado_casa": null,
    "placar_agregado_fora": null,
    "classificado": null
  }
]
```

Campos reconhecidos:

| Campo | Descrição |
|---|---|
| `equipe_casa`, `equipe_fora` | Nomes das equipes |
| `campeonato` | Competição |
| `fase` | Fase ou rodada, quando disponível |
| `horario` | Horário exibido no card |
| `status` | Estado da partida |
| `placar_casa`, `placar_fora` | Placar principal |
| `escudo_casa`, `escudo_fora` | URLs de imagem |
| `placar_intervalo_casa`, `placar_intervalo_fora` | Placar do intervalo |
| `placar_agregado_casa`, `placar_agregado_fora` | Placar agregado |
| `classificado` | Equipe classificada, quando aplicável |

O frontend reconhece estados equivalentes a ao vivo, finalizado, adiado e cancelado, inclusive alguns termos em inglês.

## 5. GET /api/preferencias

Retorna as preferências salvas. A resposta pode ser o objeto diretamente ou um objeto que contenha a propriedade `preferencias`.

Exemplo compatível:

```json
{
  "preferencias": {
    "timeBrasil": "Time brasileiro",
    "timeEuropa": "Time europeu",
    "jogadorFavorito": "Jogador"
  }
}
```

O cliente também reconhece as variantes `time_brasil`, `time_europa` e `jogador_favorito`.

## 6. POST /api/preferencias

Recebe JSON com os três campos obrigatórios do formulário.

Requisição:

```http
POST /api/preferencias
Content-Type: application/json
```

```json
{
  "timeBrasil": "Time brasileiro",
  "timeEuropa": "Time europeu",
  "jogadorFavorito": "Jogador"
}
```

O frontend verifica `response.ok`; portanto, espera um status HTTP de sucesso para considerar a operação concluída. O corpo de resposta não é consumido pelo código cliente.

Resposta recomendada para a futura implementação:

```json
{
  "success": true,
  "preferencias": {
    "timeBrasil": "Time brasileiro",
    "timeEuropa": "Time europeu",
    "jogadorFavorito": "Jogador"
  }
}
```

Essa resposta é uma recomendação de contrato, não uma resposta capturada do servidor.

## 7. Regras gerais recomendadas

- Retornar JSON com `Content-Type: application/json`.
- Usar `200` para consultas bem-sucedidas, `201` ou `200` para gravações e códigos `4xx/5xx` para erros.
- Validar tipo, tamanho e conteúdo de todos os campos recebidos.
- Definir limites e paginação se o volume de notícias ou partidas crescer.
- Não retornar credenciais ou mensagens internas de infraestrutura.
- Normalizar datas e fusos horários; documentar o fuso utilizado.
- Validar URLs de fontes e escudos, aceitando apenas esquemas seguros, como HTTPS.

## 8. Pendente para concluir o contrato

- Implementar e versionar os quatro handlers.
- Definir se as preferências são globais ou associadas a uma conta autenticada.
- Definir códigos de erro e formato uniforme de erro.
- Definir política de cache e atualização das fontes.
- Adicionar testes de contrato.
