## Componente: ReservationForm

Formulário para criação de reserva de assentos.

### Props
```
<ReservationForm
  scheduleId="uuid"
  defaultSeats={1}
  onSubmit={async ({ seats, notes }) => {}}
  onCancel={() => {}}
/>
```

### Tipos
```
type SubmitData = { seats: number; notes?: string }
```

### Regras de validação
- `seats` inteiro >= 1 e <= assentos disponíveis
- `notes` opcional, até 200 caracteres

### Exemplo
```tsx
import { ReservationForm } from '@rotacerta/ui'
import { client } from '../sdk'

export function Reserva({ scheduleId }: { scheduleId: string }) {
  return (
    <ReservationForm
      scheduleId={scheduleId}
      defaultSeats={1}
      onSubmit={async ({ seats, notes }) => {
        await client.reservations.create({ schedule_id: scheduleId, seats, notes }, { idempotencyKey: crypto.randomUUID() })
        alert('Reserva criada!')
      }}
      onCancel={() => history.back()}
    />
  )
}
```