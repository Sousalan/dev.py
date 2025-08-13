## Componente: ScheduleList

Lista horários com filtros e ação de reservar.

### Props
```
<ScheduleList
  schedules={[]}
  onReserve={(schedule) => {}}
  onFilterChange={(filters) => {}}
  loading={false}
/>
```

### Tipos
```
type Schedule = {
  id: string
  driver_name: string
  vehicle_plate: string
  departure_time: string
  price_cents: number
  available_seats: number
}

type Filters = {
  from_city?: string
  to_city?: string
  date?: string // YYYY-MM-DD
}
```

### Exemplo
```tsx
import { useEffect, useState } from 'react'
import { ScheduleList } from '@rotacerta/ui'
import { client } from '../sdk'

export function Lista() {
  const [filters, setFilters] = useState({ from_city: 'Cidade A', to_city: 'Cidade B' })
  const [loading, setLoading] = useState(false)
  const [schedules, setSchedules] = useState([])

  useEffect(() => {
    setLoading(true)
    client.schedules.list(filters).then(r => setSchedules(r.data)).finally(() => setLoading(false))
  }, [filters])

  return (
    <ScheduleList
      schedules={schedules}
      loading={loading}
      onFilterChange={(f) => setFilters({ ...filters, ...f })}
      onReserve={(s) => client.reservations.create({ schedule_id: s.id, seats: 1 })}
    />
  )
}
```