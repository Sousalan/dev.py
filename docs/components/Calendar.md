## Componente: Calendar

Exibe um calendário com horários disponíveis por dia e rota.

### Props
```
<Calendar
  date={new Date()}
  fromCity="Cidade A"
  toCity="Cidade B"
  onSelectDate={(date) => {}}
  onSelectSchedule={(schedule) => {}}
  fetchSchedules={async ({ date, fromCity, toCity }) => Promise<Schedule[]>}
  locale="pt-BR"
/>
```

### Tipos
```
type Schedule = {
  id: string
  departure_time: string
  available_seats: number
  price_cents: number
  currency: string
}
```

### Exemplo (React)
```tsx
import { useState } from 'react'
import { Calendar } from '@rotacerta/ui'
import { client } from '../sdk'

export function BuscaCalendario() {
  const [fromCity, setFromCity] = useState('Cidade A')
  const [toCity, setToCity] = useState('Cidade B')

  return (
    <Calendar
      fromCity={fromCity}
      toCity={toCity}
      fetchSchedules={async ({ date, fromCity, toCity }) => {
        const r = await client.schedules.list({ date: date.toISOString().slice(0,10), from_city: fromCity, to_city: toCity })
        return r.data
      }}
      onSelectSchedule={(s) => console.log('selecionado', s.id)}
      locale="pt-BR"
    />
  )
}
```