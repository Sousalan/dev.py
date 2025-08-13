## Reservas

Reservas garantem assentos em um horário específico.

### Criar reserva
`POST /v1/reservations`

Headers:
- `Authorization: Bearer <token>`
- Recomendado: `Idempotency-Key: <uuid>`

Body:
```
{ "schedule_id": "uuid", "seats": 1, "notes?": "pegar no ponto central" }
```

Response 201:
```
{
  "id": "uuid",
  "schedule_id": "uuid",
  "passenger": { "id": "uuid", "name": "Dona Célia" },
  "driver": { "id": "uuid", "name": "Rafael" },
  "seats": 1,
  "status": "confirmed",
  "created_at": "2025-01-31T12:00:00Z"
}
```

### Obter reserva
`GET /v1/reservations/{reservation_id}`

### Listar reservas
`GET /v1/reservations?passenger_id=&driver_id=&schedule_id=&status=&from=&to=&limit=&cursor=`

### Atualizar reserva
`PATCH /v1/reservations/{reservation_id}`

Body:
```
{ "seats?": 2, "notes?": "novo ponto" }
```

### Cancelar reserva
`POST /v1/reservations/{reservation_id}/cancel`

Body:
```
{ "reason": "plano mudou" }
```

### Status possíveis
- `confirmed`: assentos garantidos
- `canceled`: cancelada por passageiro, motorista ou sistema
- `completed`: viagem realizada

### Webhooks relacionados
- `reservation.created`
- `reservation.canceled`
- `reservation.updated`

Veja `../guides/webhooks.md`.