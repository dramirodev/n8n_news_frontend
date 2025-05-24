Extraer los valores de un objeto en TypeScript puede ser confuso. Pero con la ayuda de `as const`, podemos asegurarnos de obtener **valores literales exactos**, útiles para validaciones, uniones y más.

---

## 📚 Temas incluidos y explicación extendida

### 1. Declarar objeto `as const`
```ts
const estados = {
  activo: 'ACTIVO',
  inactivo: 'INACTIVO'
} as const;
```
> ⚠️ **Error común**: olvidar `as const` y obtener `string` genérico.

---

### 2. Extraer valores como unión
```ts
type Estados = typeof estados[keyof typeof estados];
// 'ACTIVO' | 'INACTIVO'
```

---

### 3. Tipar funciones que reciben uno de los valores
```ts
function cambiarEstado(e: Estados) { ... }
```
> ⚠️ **Error común**: usar string sin unión específica.

---

### 4. Uso con enums-like objetos
```ts
const roles = {
  admin: 'ADMIN',
  user: 'USER',
  guest: 'GUEST'
} as const;

type Role = typeof roles[keyof typeof roles];
```

---

## 🧠 Tabla resumen
| Técnica | Resultado | Nota |
|---------|-----------|------|
| `as const` | literales | fija valores |
| `typeof obj[keyof typeof obj]` | unión de valores | tipos exactos |
| funciones con unión | restringidas | más seguras |

---

## 🧙‍♀️ Moraleja
> *Para controlar los valores, primero debes hacerlos constantes.*