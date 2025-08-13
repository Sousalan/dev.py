## Quickstart

Este guia mostra como um passageiro (Dona Célia) e um motorista (Rafael) utilizam o Rota Certa.

### 1) Criar conta
```
curl -X POST "https://api.rotacerta.com/v1/auth/register" \
  -H "Content-Type: application/json" \
  -d '{
    "role": "passenger",
    "name": "Dona Célia",
    "email": "celia@example.com",
    "phone": "+5531999999999",
    "password": "SenhaForte123"
  }'
```

### 2) Login e token
```
TOKEN=$(curl -s -X POST https://api.rotacerta.com/v1/auth/login \
  -H 'Content-Type: application/json' \
  -d '{"email":"celia@example.com","password":"SenhaForte123"}' | jq -r .access_token)
```

### 3) Buscar horários (passageiro)
```
curl "https://api.rotacerta.com/v1/schedules?from_city=Cidade%20A&to_city=Cidade%20B&date=2025-02-01" \
  -H "Authorization: Bearer $TOKEN"
```

### 4) Reservar vaga (idempotente)
```
curl -X POST https://api.rotacerta.com/v1/reservations \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -H "Idempotency-Key: $(uuidgen)" \
  -d '{"schedule_id":"<uuid>","seats":1}'
```

### 5) Publicar horário (motorista)
```
curl -X POST https://api.rotacerta.com/v1/drivers/<driver_id>/schedules \
  -H "Authorization: Bearer $TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "route_id": "<uuid>",
    "departure_time": "2025-02-01T06:30:00-03:00",
    "estimated_arrival_time": "2025-02-01T08:00:00-03:00",
    "price_cents": 1500,
    "currency": "BRL",
    "vehicle_id": "<uuid>",
    "total_seats": 4
  }'
```

### 6) Notificações em tempo real (SSE)
```
curl -N "https://api.rotacerta.com/v1/realtime/sse?channels=user:<user_id>" -H "Authorization: Bearer $TOKEN"
```