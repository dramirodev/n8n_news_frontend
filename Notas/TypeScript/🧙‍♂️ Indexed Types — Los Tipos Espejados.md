

Los **Indexed Types** permiten acceder a tipos dentro de estructuras usando índices de tipo clave (`keyof`) o numéricos. Son la base para introspección, mapeo y composición de tipos complejos.

---

## 📚 Temas incluidos y explicación extendida

### 1. Acceso con `T[K]`
```ts
type User = { id: number; name: string };
type Nombre = User['name']; // string
```
> ⚠️ **Error común**: intentar acceder con claves no existentes.

---

### 2. Composición con `keyof`
```ts
type Claves = keyof User; // 'id' | 'name'
type Valores = User[Claves]; // number | string
```
> ⚠️ **Error común**: olvidar que accediendo con una unión, se produce una unión de tipos.

---

### 3. Uso con tipos genéricos
```ts
type ValorDe<T, K extends keyof T> = T[K];
```
> ⚠️ **Error común**: no restringir K con `keyof T`.

---

## 🧠 Tabla resumen
| Sintaxis | Significado | Ejemplo |
|---------|-------------|---------|
| `T[K]` | tipo de propiedad `K` en `T` | `User['id']` |
| `T[keyof T]` | unión de tipos de todas las propiedades | `User['id' | 'name']` |
| `keyof T` | unión de claves de `T` | `'id' | 'name'` |

---

## 🧙‍♀️ Moraleja
> *Los indexed types son como los espejos mágicos: te dejan ver el interior de una estructura… si haces la pregunta correcta.*