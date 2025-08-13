## Paginação

A API usa paginação baseada em cursor.

### Requisição
```
GET /v1/schedules?limit=25&cursor=eyJwYWdlIjoyfQ==
```

### Resposta
```
{
  "data": [ /* itens */ ],
  "next_cursor": "eyJwYWdlIjozfQ=="
}
```

### Boas práticas
- Sempre preserve o `limit` entre chamadas
- Pare quando `next_cursor` estiver ausente
- Não tente decodificar o cursor; trate-o como opaco