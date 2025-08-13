## Componente: PassengerDashboard

Painel do passageiro para buscar horários, gerenciar reservas e avaliações.

### Recursos
- Busca por origem/destino/data
- Calendário e lista de horários
- Minhas reservas (histórico e futuras)
- Notificações em tempo real
- Avaliar motoristas

### Exemplo de composição
```tsx
<PassengerDashboard
  listSchedules={(q) => client.schedules.list(q)}
  listMyReservations={(passengerId, q) => client.passengers.listReservations(passengerId, q)}
  createReservation={(data) => client.reservations.create(data, { idempotencyKey: crypto.randomUUID() })}
  listNotifications={(q) => client.notifications.list(q)}
  subscribe={(channels, onEvent) => client.realtime.subscribeSSE({ channels }, onEvent)}
  rateDriver={(data) => client.ratings.create(data)}
/>
```