## Visão Geral da API

A API do Rota Certa segue o estilo REST, com recursos versionados sob o prefixo `/v1`. Respostas retornam JSON. Tempos são ISO 8601 com timezone (ex.: `2025-01-31T12:34:56-03:00`).

### Versionamento
- URL versionada: `/v1`
- Quebras de compatibilidade só em novas versões (ex.: `/v2`)

### Autenticação
- Header: `Authorization: Bearer <token>`
- Obtenha tokens em `POST /v1/auth/login` ou `POST /v1/auth/register`
- Renove com `POST /v1/auth/refresh`

### Segurança
- HTTPS obrigatório
- Suporte a `Idempotency-Key` em operações de escrita críticas (reservas)
- Recursos com controle de acesso (passageiro vs motorista)

### Paginação
- Cursor baseada em tokens
- Query params: `limit` (1–100, padrão 25), `cursor` (fornecido pela resposta anterior)
- Resposta inclui `next_cursor` quando houver mais itens

### Filtros e Ordenação
- Filtros por campos com `?campo=valor`
- Intervalos de data: `?from=2025-01-01T00:00:00Z&to=2025-01-31T23:59:59Z`
- Ordenação: `?sort=campo` e `?order=asc|desc` (padrão `asc`)

### Erros
Formato padrão de erro:

```
{
  "error": {
    "code": "string",
    "message": "string descritiva para humanos",
    "details": { "campo?": "explicação opcional" },
    "request_id": "uuid"
  }
}
```

- Códigos comuns: `bad_request`, `unauthorized`, `forbidden`, `not_found`, `conflict`, `rate_limited`, `validation_error`, `internal`.

### Rate Limits
- Cabeçalhos de resposta:
  - `X-RateLimit-Limit`: capacidade do período
  - `X-RateLimit-Remaining`: restante no período
  - `X-RateLimit-Reset`: epoch seconds para reset
- Restrições típicas: 60 req/min por token para endpoints comuns

### Idempotência
- Envie `Idempotency-Key: <uuid>` em `POST /v1/reservations`
- Repetições com a mesma chave retornam a mesma resposta
- Expiração típica: 24 horas

### Convenções
- `snake_case` em atributos JSON
- `uuid` para identificadores públicos
- `price_cents` inteiro em centavos, `currency` ISO 4217 (ex.: `BRL`)
- `status` com enum documentado por recurso