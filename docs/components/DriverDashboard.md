## Componente: DriverDashboard

Painel para motoristas gerenciarem veículos, horários e reservas.

### Recursos
- Mostrar métricas: ocupação média, próximas viagens, avaliações
- CRUD de veículos
- Publicação e edição de horários
- Lista de reservas recebidas
- Notificações em tempo real

### Integrações
- API `drivers`, `schedules`, `reservations`, `notifications`
- Realtime via SSE/WebSocket

### Exemplo de composição
```tsx
<DriverDashboard
  fetchDriver={id => client.drivers.get(id)}
  fetchVehicles={id => client.drivers.listVehicles(id)}
  createVehicle={(id, data) => client.drivers.createVehicle(id, data)}
  listSchedules={(id, q) => client.drivers.listSchedules(id, q)}
  createSchedule={(id, data) => client.drivers.createSchedule(id, data)}
  cancelSchedule={(id, scheduleId, data) => client.drivers.cancelSchedule(id, scheduleId, data)}
  listReservations={(id, q) => client.drivers.listReservations?.(id, q)}
  subscribe={(channels, onEvent) => client.realtime.subscribeSSE({ channels }, onEvent)}
/>
```