Las **const assertions** (`as const`) permiten a TypeScript inferir el tipo más literal e inmutable posible. Es decir, no solo el valor, sino su forma final.

Esto es vital para:
- Tuplas exactas
- Objetos como enums literales
- Inferencia de valores con precisión quirúrgica

---

## 📚 Temas incluidos y explicación extendida

### 1. Literales exactos
```ts
const saludo = 'hola' as const; // tipo: 'hola'
```
> ⚠️ **Error común**: pensar que `const` y `as const` hacen lo mismo.

---

### 2. Tuplas fijas
```ts
const par = [10, 20] as const; // tipo: readonly [10, 20]
```
> ⚠️ **Error común**: asumir que se puede modificar luego.

---

### 3. Objetos inmutables
```ts
const config = {
  modo: 'oscuro',
  tamaño: 'grande'
} as const;
```
> ⚠️ **Error común**: intentar reasignar propiedades

---

### 4. Uso en discriminated unions
```ts
const evento = { tipo: 'clic' } as const;
```
> ⚠️ **Error común**: no usar `as const` y perder precisión en `tipo`.

---

## 🧠 Tabla resumen
| Caso | Resultado | Precisión |
|------|-----------|-----------|
| string `as const` | literal | ✅ |
| tupla `as const` | readonly tuple | ✅ |
| objeto | propiedades readonly | ✅ |
| enum-like | perfecto | ✅ |

---

## 🧙‍♀️ Moraleja
> *`as const` es el conjuro definitivo para sellar tipos como verdades inmutables.*