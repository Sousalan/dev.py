## Webhooks

### Registro
`POST /v1/webhooks/endpoints`
```
{ "url": "https://example.com/webhooks/rotacerta", "events": ["reservation.created","reservation.canceled"] }
```

### Segurança
- Assinatura HMAC SHA-256 no header `X-RotaCerta-Signature`
- Assinatura calculada sobre o corpo bruto usando o `secret` do endpoint
- Valide `t` (timestamp) para tolerância a replays (ex.: 5 min)

### Exemplo de entrega
Headers:
```
X-RotaCerta-Event: reservation.created
X-RotaCerta-Timestamp: 1738400000
X-RotaCerta-Signature: t=1738400000,v1=hex
```

Body:
```
{ "id":"evt_123", "type":"reservation.created", "data": { "reservation_id":"uuid" } }
```

### Retentativas
- Backoff exponencial até 24h
- 2xx confirma entrega

### Eventos suportados
- `reservation.created`, `reservation.canceled`, `reservation.updated`
- `schedule.updated`