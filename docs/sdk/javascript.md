## SDK JavaScript/TypeScript

Instale:
```
npm install @rotacerta/sdk
```

Inicialização:
```ts
import { RotaCerta } from '@rotacerta/sdk'

const client = new RotaCerta({
  baseUrl: 'https://api.rotacerta.com/v1',
  token: process.env.ROTACERTA_TOKEN,
})
```

### Autenticação
```ts
const { accessToken } = await client.auth.login({ email: 'user@example.com', password: 'secret' })
client.setToken(accessToken)
```

### Buscar horários
```ts
const schedules = await client.schedules.list({ from_city: 'Cidade A', to_city: 'Cidade B', date: '2025-02-01' })
```

### Criar reserva (com idempotência)
```ts
await client.reservations.create(
  { schedule_id: 'uuid', seats: 1 },
  { idempotencyKey: crypto.randomUUID() }
)
```

### Assinar notificações (SSE)
```ts
const unsubscribe = client.realtime.subscribeSSE({ channels: [`user:${userId}`] }, (event) => {
  console.log('event', event.type, event.data)
})
// ...
unsubscribe()
```

### API pública do SDK
- `new RotaCerta({ baseUrl?, token? })`
- `client.setToken(token: string)`
- `client.auth.register(data)`
- `client.auth.login(data)`
- `client.auth.refresh(data)`
- `client.users.me()`
- `client.passengers.get(passengerId)`
- `client.passengers.update(passengerId, data)`
- `client.passengers.listReservations(passengerId, query)`
- `client.drivers.get(driverId)`
- `client.drivers.listVehicles(driverId)`
- `client.drivers.createVehicle(driverId, data)`
- `client.drivers.createSchedule(driverId, data)`
- `client.drivers.listSchedules(driverId, query)`
- `client.drivers.cancelSchedule(driverId, scheduleId, data)`
- `client.routes.list(query)`
- `client.routes.get(routeId)`
- `client.schedules.list(query)`
- `client.schedules.get(scheduleId)`
- `client.schedules.update(scheduleId, data)`
- `client.schedules.cancel(scheduleId, data)`
- `client.reservations.create(data, options?)`
- `client.reservations.get(reservationId)`
- `client.reservations.list(query)`
- `client.reservations.update(reservationId, data)`
- `client.reservations.cancel(reservationId, data)`
- `client.notifications.list(query)`
- `client.notifications.markAsRead(notificationId)`
- `client.ratings.create(data)`
- `client.ratings.listForDriver(driverId, query)`
- `client.ratings.listForPassenger(passengerId, query)`
- `client.realtime.subscribeSSE({ channels }, onEvent)`
- `client.realtime.connectWebSocket()`