## Modelos de Dados (Schemas)

### User
```
{
  "id": "uuid",
  "role": "passenger|driver|admin",
  "name": "string",
  "email": "string",
  "phone": "string",
  "created_at": "ISO8601",
  "updated_at": "ISO8601"
}
```

### Driver
```
{
  "id": "uuid",
  "name": "string",
  "email": "string",
  "phone": "string",
  "cooperative": { "id": "uuid", "name": "string" },
  "rating_avg": 0.0,
  "vehicles": [ { "id": "uuid", "plate": "ABC1D23", "model": "string", "color": "string", "seats": 4 } ]
}
```

### Passenger
```
{
  "id": "uuid",
  "name": "string",
  "email": "string",
  "phone": "string",
  "default_pickup_place?": "string"
}
```

### Route
```
{
  "id": "uuid",
  "from_city": "string",
  "to_city": "string",
  "stops": ["string"],
  "distance_km": 0,
  "estimated_duration_min": 0
}
```

### Schedule
```
{
  "id": "uuid",
  "route_id": "uuid",
  "driver": { "id": "uuid", "name": "string" },
  "vehicle": { "id": "uuid", "plate": "string", "seats": 4 },
  "departure_time": "ISO8601",
  "estimated_arrival_time": "ISO8601",
  "price_cents": 0,
  "currency": "BRL",
  "available_seats": 0,
  "status": "scheduled|in_progress|completed|canceled"
}
```

### Reservation
```
{
  "id": "uuid",
  "schedule_id": "uuid",
  "passenger": { "id": "uuid", "name": "string" },
  "driver": { "id": "uuid", "name": "string" },
  "seats": 1,
  "status": "confirmed|canceled|completed",
  "notes?": "string",
  "created_at": "ISO8601"
}
```

### Notification
```
{
  "id": "uuid",
  "type": "reservation.created|reservation.canceled|schedule.updated|vehicle.arriving",
  "title": "string",
  "body": "string",
  "read": false,
  "data": { "reservation_id?": "uuid", "schedule_id?": "uuid" },
  "created_at": "ISO8601"
}
```

### Rating
```
{
  "id": "uuid",
  "reservation_id": "uuid",
  "author": { "id": "uuid", "role": "passenger|driver" },
  "target": { "type": "driver|passenger", "id": "uuid" },
  "score": 1,
  "comment?": "string",
  "created_at": "ISO8601"
}
```