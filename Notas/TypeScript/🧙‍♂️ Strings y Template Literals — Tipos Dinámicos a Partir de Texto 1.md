

TypeScript permite construir, combinar y transformar **tipos literales de strings** mediante una poderosa sintaxis de Template Literal Types.

Esto abre las puertas a construir APIs con inferencia inteligente, validadores de rutas, patrones reutilizables y más.

---

## 📚 Temas incluidos y explicación extendida

### 1. Concatenación básica
```ts
type Ruta = `/${string}`; // cualquier string que empiece con /
```

### 2. Unión e interpolación
```ts
type Roles = 'admin' | 'user';
type RutaPrivada = `/${Roles}/dashboard`; // '/admin/dashboard' | '/user/dashboard'
```

### 3. Extracción con `infer`
```ts
type ExtraerID<T> = T extends `user/${infer ID}` ? ID : never;
type ID = ExtraerID<'user/123'>; // '123'
```

---

## 🧠 Tabla resumen
| Técnica | Resultado | Nota |
|---------|-----------|------|
| `