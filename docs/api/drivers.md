## Motoristas

### Obter perfil do motorista
`GET /v1/drivers/{driver_id}`

Response 200:
```
{
  "id": "uuid",
  "name": "string",
  "email": "string",
  "phone": "string",
  "cooperative": { "id": "uuid", "name": "string" },
  "rating_avg": 4.8,
  "created_at": "2025-01-31T12:00:00Z"
}
```

### Veículos do motorista
- Listar: `GET /v1/drivers/{driver_id}/vehicles`
- Criar: `POST /v1/drivers/{driver_id}/vehicles`

Body:
```
{ "plate": "ABC1D23", "model": "Fiat Uno", "color": "prata", "seats": 4 }
```

### Publicar horário (criar viagem)
`POST /v1/drivers/{driver_id}/schedules`

Body:
```
{
  "route_id": "uuid",
  "departure_time": "2025-02-01T06:30:00-03:00",
  "estimated_arrival_time": "2025-02-01T08:00:00-03:00",
  "price_cents": 1500,
  "currency": "BRL",
  "vehicle_id": "uuid",
  "total_seats": 4,
  "stops?": [ { "name": "Ponto A", "time": "2025-02-01T07:10:00-03:00" } ]
}
```

Response 201:
```
{ "id": "uuid", "status": "scheduled", "available_seats": 4, "route_id": "uuid", "departure_time": "..." }
```

### Gerenciar horários
- Listar: `GET /v1/drivers/{driver_id}/schedules?status=&from=&to=`
- Atualizar: `PATCH /v1/drivers/{driver_id}/schedules/{schedule_id}`
- Cancelar: `POST /v1/drivers/{driver_id}/schedules/{schedule_id}/cancel`

### Reservas recebidas
`GET /v1/drivers/{driver_id}/reservations?status=&from=&to=`

### Avaliar passageiros
`POST /v1/drivers/{driver_id}/ratings`

Body:
```
{ "reservation_id": "uuid", "score": 5, "comment?": "Pontual e educado." }
```