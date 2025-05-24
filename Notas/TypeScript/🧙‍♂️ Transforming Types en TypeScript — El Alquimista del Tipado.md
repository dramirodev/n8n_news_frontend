

Los **Transforming Types** son los hechizos avanzados de transmutación: convertir objetos en uniones, uniones en arrays, listas en tuplas, y viceversa. Dominar esta magia te permite remodelar estructuras tipadas para que se ajusten a cualquier hechizo.

---

## 📚 Temas incluidos y explicación extendida

### 1. De objeto a unión
```ts
type ToUnion<T> = T[keyof T];
```
> ⚠️ **Error común**: asumir que cada propiedad es del mismo tipo.

---

### 2. De unión a objeto
```ts
type FromUnion<T extends string> = {
  [K in T]: K;
};
```
> ⚠️ **Error común**: olvidar que necesitas un `extends string` para claves válidas.

---

### 3. Object entries como tuplas
```ts
type Entry<T> = {
  [K in keyof T]: [K, T[K]];
}[keyof T];
```
> ⚠️ **Error común**: no saber que esto genera una unión de tuplas.

---

### 4. De tupla a unión
```ts
type FromTuple<T extends any[]> = T[number];
```
> ⚠️ **Error común**: no saber que `[number]` accede a todos los índices.

---

### 5. Invertir clave/valor de objeto
```ts
type Invert<T> = {
  [K in keyof T as T[K] extends string | number ? `${T[K]}` : never]: K;
};
```
> ⚠️ **Error común**: no considerar claves válidas.

---

## 🧠 Tabla resumen
| Transformación | Tipo | Resultado | Error común |
|---|---|---|---|
| Obj → unión | `T[keyof T]` | unión de valores | No usar `keyof` |
| Unión → obj | `Record<T, T>` | clave igual a valor | Unión no string |
| Obj → entries | `[K, T[K]]` | unión de pares | Asumir array |
| Tupla → unión | `T[number]` | unión de elementos | Acceso incorrecto |
| Invertir | valor → clave | flip dinámico | Valores no string |

---

## 🧙‍♀️ Moraleja
> *Transformar tipos es como transmutar oro desde plomo: necesitas precisión, o terminarás con errores y alquimia explosiva.*