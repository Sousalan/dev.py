## Realtime (SSE e WebSocket)

### SSE (Server-Sent Events)
- Endpoint: `GET /v1/realtime/sse?channels=...`
- Header obrigatório: `Authorization: Bearer <token>`
- Múltiplos canais separados por vírgula, ex.: `user:{user_id}`

Exemplo cURL:
```
curl -N "https://api.rotacerta.com/v1/realtime/sse?channels=user:<user_id>" \
  -H "Authorization: Bearer $TOKEN"
```

Formato de evento:
```
event: reservation.created
data: {"reservation_id":"uuid", "schedule_id":"uuid"}
```

### WebSocket
- URL: `wss://api.rotacerta.com/v1/realtime/ws`
- Autenticação: envie `{ type: "auth", token: "<jwt>" }` ao conectar
- Assinatura de canais: `{ type: "subscribe", channels: ["user:<user_id>"] }`

Exemplo JS:
```js
const ws = new WebSocket('wss://api.rotacerta.com/v1/realtime/ws')
ws.onopen = () => {
  ws.send(JSON.stringify({ type: 'auth', token }))
  ws.send(JSON.stringify({ type: 'subscribe', channels: [`user:${userId}`] }))
}
ws.onmessage = (msg) => {
  const event = JSON.parse(msg.data)
  console.log('event', event.type, event.data)
}
```

### Tipos de eventos
- `reservation.created`
- `reservation.canceled`
- `reservation.updated`
- `schedule.updated`
- `vehicle.arriving`