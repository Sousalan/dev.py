## Componente: RatingWidget

Widget de estrelas para avaliação pós-viagem.

### Props
```
<RatingWidget
  defaultValue={0}
  onChange={(score) => {}}
  readOnly={false}
  max={5}
/>
```

### Exemplo
```tsx
<RatingWidget
  defaultValue={0}
  onChange={(score) => client.ratings.create({ reservation_id, target: { type: 'driver', id: driverId }, score })}
/>
```