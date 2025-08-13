## Rotas

Rotas representam ligações entre localidades (origem-destino) com metadados úteis para busca.

### Buscar rotas
`GET /v1/routes?query=&from_city=&to_city=&limit=&cursor=`

Response 200:
```
{
  "data": [
    { "id": "uuid", "from_city": "Cidade A", "to_city": "Cidade B", "distance_km": 120, "estimated_duration_min": 90 }
  ],
  "next_cursor": "string?"
}
```

### Obter rota
`GET /v1/routes/{route_id}`

### Criar/atualizar rota (admin/cooperativa)
- Criar: `POST /v1/routes`
- Atualizar: `PUT /v1/routes/{route_id}`

Body:
```
{
  "from_city": "Cidade A",
  "to_city": "Cidade B",
  "stops?": ["Ponto 1", "Ponto 2"],
  "distance_km?": 120,
  "estimated_duration_min?": 90
}
```