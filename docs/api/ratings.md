## Avaliações

Passageiros e motoristas podem avaliar-se após viagens concluídas.

### Avaliar motorista (pelo passageiro)
`POST /v1/ratings`

Body:
```
{ "reservation_id": "uuid", "target": { "type": "driver", "id": "uuid" }, "score": 5, "comment?": "muito pontual" }
```

### Avaliar passageiro (pelo motorista)
`POST /v1/ratings`

Body:
```
{ "reservation_id": "uuid", "target": { "type": "passenger", "id": "uuid" }, "score": 5, "comment?": "educado e pontual" }
```

### Listar avaliações de um motorista
`GET /v1/drivers/{driver_id}/ratings?limit=&cursor=`

Response 200:
```
{
  "data": [ { "id": "uuid", "score": 5, "comment": "muito pontual", "created_at": "..." } ],
  "average": 4.8,
  "count": 120,
  "next_cursor": "string?"
}
```

### Listar avaliações de um passageiro
`GET /v1/passengers/{passenger_id}/ratings?limit=&cursor=`

### Regras
- `score` inteiro de 1 a 5
- Uma avaliação por reserva por avaliador