## Notificações

Notificações informam mudanças relevantes (reservas, atualizações de horários, chegada do veículo).

### Listar notificações
`GET /v1/notifications?user_id=&unread_only=&limit=&cursor=`

Response 200:
```
{
  "data": [
    {
      "id": "uuid",
      "type": "reservation.confirmed",
      "title": "Reserva confirmada",
      "body": "Sua reserva foi confirmada para 06:30",
      "created_at": "2025-02-01T06:00:00-03:00",
      "read": false,
      "data": { "reservation_id": "uuid", "schedule_id": "uuid" }
    }
  ],
  "next_cursor": "string?"
}
```

### Marcar como lida
`POST /v1/notifications/{notification_id}/read`

### Apagar
`DELETE /v1/notifications/{notification_id}`

### Tempo real
- SSE: `GET /v1/realtime/sse?channels=user:{user_id}`
- WebSocket: `wss://api.rotacerta.com/v1/realtime/ws` (enviar `SUBSCRIBE user:{user_id}`)

Veja `../guides/realtime.md` para detalhes e exemplos.