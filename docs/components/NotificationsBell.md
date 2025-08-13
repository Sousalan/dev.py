## Componente: NotificationsBell

Mostra um sino com contagem de notificações não lidas e menu de itens.

### Props
```
<NotificationsBell
  count={3}
  items={[{ id: 'uuid', title: 'Reserva confirmada', created_at: '...' }]}
  onOpen={() => {}}
  onItemClick={(item) => {}}
  onMarkAllRead={() => {}}
/>
```

### Exemplo
```tsx
<NotificationsBell
  count={unread}
  items={notifications}
  onOpen={() => setUnread(0)}
  onItemClick={(n) => navigate(`/reservas/${n.data?.reservation_id}`)}
  onMarkAllRead={() => notifications.forEach(n => client.notifications.markAsRead(n.id))}
/>
```