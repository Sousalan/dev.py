## Autenticação

### Registro de Usuário
`POST /v1/auth/register`

Cria uma conta de passageiro ou motorista.

Body:
```
{
  "role": "passenger" | "driver",
  "name": "string",
  "email": "user@example.com",
  "phone": "+55XXXXXXXXXXX",
  "password": "min 8 chars"
}
```

Response 201:
```
{
  "user": {
    "id": "uuid",
    "role": "passenger",
    "name": "string",
    "email": "user@example.com",
    "phone": "+55...",
    "created_at": "2025-01-31T12:00:00Z"
  },
  "token": { "access_token": "jwt", "expires_in": 3600, "refresh_token": "jwt" }
}
```

Exemplo cURL:
```
curl -X POST "https://api.rotacerta.com/v1/auth/register" \
  -H "Content-Type: application/json" \
  -d '{
    "role": "passenger",
    "name": "Dona Célia",
    "email": "celia@example.com",
    "phone": "+5531999999999",
    "password": "senhaForte123"
  }'
```

### Login
`POST /v1/auth/login`

Body:
```
{
  "email": "user@example.com",
  "password": "string"
}
```

Response 200:
```
{ "access_token": "jwt", "expires_in": 3600, "refresh_token": "jwt" }
```

### Refresh Token
`POST /v1/auth/refresh`

Body:
```
{ "refresh_token": "jwt" }
```

Response 200:
```
{ "access_token": "jwt", "expires_in": 3600 }
```

### Logout
`POST /v1/auth/logout`

Header: `Authorization: Bearer <access_token>`

Body opcional:
```
{ "refresh_token": "jwt" }
```

### Perfil Atual
`GET /v1/users/me`

Retorna o usuário autenticado.

Response 200:
```
{
  "id": "uuid",
  "role": "passenger|driver",
  "name": "string",
  "email": "string",
  "phone": "string"
}
```