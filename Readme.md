<img tile="Cover" src="/cover.png" alt="Cover" > 

# Real Time Polls 
Sistema de votação em tempo real onde usuários podem criar uma enquete e votarem. O sistema gera um "ranking" entre as opções e atualiza os votos em tempo real.

A aplicação foi desenvolvida com NodeJS, Typescript, utilizando o Prisma, PostgreSQL e Redis.

## Requisitos
- Docker;
- Node.js.

## Setup
Após clonar o repositório, execute:
```
$ npm install
$ docker compose up -d
$ npm run dev
```

## Endpoints
### POST /polls
Criar uma nova enquete

<strong>Request body</strong>

```json
{
  "title": "Qual o seu framework web da empresa?",
  "options": [
    "NextJS",
    "VueJS",
    "ReactJS",
  ]
}
```

<strong>Response body</strong>
```json
{
  "pollId": "194cef63-2ccf-46a3-aad1-aa94b2bc89b0"
}
```

### GET /polls/:pollId
Listar dados de apenas uma enquete

<strong>Response body</strong>
```json
{
	"poll": {
		"id": "e4365599-0205-4429-9808-ea1f94062a5f",
		"title": "Qual a melhor linguagem de programação?",
		"options": [
			{
				"id": "4af3fca1-91dc-4c2d-b6aa-897ad5042c84",
				"title": "JavaScript",
				"score": 1
			},
			{
				"id": "780b8e25-a40e-4301-ab32-77ebf8c79da8",
				"title": "Java",
				"score": 0
			},
			{
				"id": "539fa272-152b-478f-9f53-8472cddb7491",
				"title": "PHP",
				"score": 0
			},
			{
				"id": "ca1d4af3-347a-4d77-b08b-528b181fe80e",
				"title": "C#",
				"score": 0
			}
		]
	}
}
```

### POST /polls/:pollId/votes
Votar em uma enquete especifica

<strong>Request body</strong>

```json
{
  "pollOptionId": "31cca9dc-15da-44d4-ad7f-12b86610fe98"
}
```

### ws /polls/:pollId/results
Listar os resultados de uma enquete

<strong>Message</strong>
```json
{
  "pollOptionId": "da9601cc-0b58-4395-8865-113cbdc42089",
  "votes": 2
}
```