## Horários e Viagens (Schedules)

Um horário representa uma viagem programada por um motorista em uma rota.

### Listar horários
`GET /v1/schedules?from_city=&to_city=&date=&from=&to=&driver_id=&route_id=&status=&limit=&cursor=`

- `status`: `scheduled|in_progress|completed|canceled`
- `date`: `YYYY-MM-DD` (filtra por data de partida local)

Response 200:
```
{
  "data": [
    {
      "id": "uuid",
      "route_id": "uuid",
      "driver": { "id": "uuid", "name": "Rafael" },
      "vehicle": { "id": "uuid", "plate": "ABC1D23", "seats": 4 },
      "departure_time": "2025-02-01T06:30:00-03:00",
      "estimated_arrival_time": "2025-02-01T08:00:00-03:00",
      "price_cents": 1500,
      "currency": "BRL",
      "available_seats": 3,
      "status": "scheduled"
    }
  ],
  "next_cursor": "string?"
}
```

Exemplo cURL:
```
curl "https://api.rotacerta.com/v1/schedules?from_city=Cidade%20A&to_city=Cidade%20B&date=2025-02-01&limit=10" \
  -H "Authorization: Bearer $TOKEN"
```

### Obter horário
`GET /v1/schedules/{schedule_id}`

### Criar horário (admin/cooperativa)
`POST /v1/schedules`

Body:
```
{
  "driver_id": "uuid",
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

### Atualizar horário
`PATCH /v1/schedules/{schedule_id}`

Body (parcial):
```
{ "departure_time?": "...", "estimated_arrival_time?": "...", "price_cents?": 1800, "stops?": [ ... ] }
```

### Cancelar horário
`POST /v1/schedules/{schedule_id}/cancel`

Body:
```
{ "reason": "chuva forte" }
```

### Reservas do horário
`GET /v1/schedules/{schedule_id}/reservations`

### Eventos em tempo real
- Assine atualizações do horário: consulte `../guides/realtime.md` para SSE/WebSocket