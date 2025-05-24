Los arrays declarados con `as const` se transforman en tuplas de **valores literales e inmutables**. Esto permite trabajar con uniones de valores directamente y asegurar validación tipada exacta.

---

## 📚 Temas incluidos y explicación extendida

### 1. Literalizar un array
```ts
const niveles = ['bajo', 'medio', 'alto'] as const;
```
> ⚠️ **Error común**: olvidar `as const` y obtener solo `string[]`

---

### 2. Inferencia como unión
```ts
type Nivel = typeof niveles[number];
// 'bajo' | 'medio' | 'alto'
```

---

### 3. Uso en validación
```ts
function configurar(nivel: Nivel) { ... }
```
> ⚠️ **Error común**: validar contra string genérico y no literal

---

## 🧠 Tabla resumen
| Técnica | Resultado | Nota |
|---------|-----------|------|
| `as const` en array | tupla literal | inferencia literal |
| `T[number]` | unión de elementos | acceso por índice |
| uso en función | parámetros restringidos | validación más segura |

---

## 🧙‍♀️ Moraleja
> *Un array sellado con `as const` no solo guarda valores: guarda verdad.*