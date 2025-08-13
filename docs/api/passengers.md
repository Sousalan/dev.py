## Passageiros

### Obter perfil do passageiro
`GET /v1/passengers/{passenger_id}`

Response 200:
```
{
  "id": "uuid",
  "name": "string",
  "email": "string",
  "phone": "string",
  "default_pickup_place": "string?",
  "created_at": "2025-01-31T12:00:00Z"
}
```

### Atualizar perfil do passageiro
`PATCH /v1/passengers/{passenger_id}`

Body:
```
{ "name?": "string", "phone?": "string", "default_pickup_place?": "string" }
```

Response 200: objeto atualizado

### Listar reservas do passageiro
`GET /v1/passengers/{passenger_id}/reservations?status=&from=&to=&limit=&cursor=`

Response 200:
```
{
  "data": [ { "id": "uuid", "schedule_id": "uuid", "seats": 1, "status": "confirmed", "created_at": "..." } ],
  "next_cursor": "string?"
}
```

### Criar reserva (atalho)
`POST /v1/passengers/{passenger_id}/reservations`

Header recomendado: `Idempotency-Key: <uuid>`

Body:
```
{ "schedule_id": "uuid", "seats": 1, "notes?": "string" }
```

Response 201: ver `Reservas`

### Notificações do passageiro
`GET /v1/passengers/{passenger_id}/notifications?limit=&cursor=&unread_only=`

Marcar como lida:
`POST /v1/passengers/{passenger_id}/notifications/{notification_id}/read`

### Avaliações feitas pelo passageiro
`GET /v1/passengers/{passenger_id}/ratings`