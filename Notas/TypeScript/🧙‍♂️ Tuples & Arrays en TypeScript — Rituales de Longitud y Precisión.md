

En el gremio de los tipos estructurados, las **tuplas** y los **arrays** son artefactos de almacenamiento que permiten organizar valores con precisión o con libertad, según la invocación.

Una tupla te ofrece **posicionalidad fija** y heterogeneidad; un array, **longitud variable** y homogeneidad. Juntos forman una de las dualidades más importantes del mundo tipado.

---

## 📚 Temas incluidos y explicación extendida

### 1. Diferencias básicas entre Tuple y Array
```ts
let t: [string, number];
let a: number[];
```
- `t` tiene longitud fija, `a` no.
- `t[0]` es `string`, `t[1]` es `number`; en `a`, todos son `number`.

> ⚠️ **Error común**: usar una tupla para almacenar más elementos de los que declara.

---

### 2. Uso de infer en tuplas
```ts
type Head<T extends any[]> = T extends [infer H, ...any[]] ? H : never;
```
> ⚠️ **Error común**: no validar que el tipo es realmente una tupla.

---

### 3. Longitud de tuplas
```ts
type Length<T extends any[]> = T['length'];
```
> ⚠️ **Error común**: asumir que todas las listas tienen una longitud concreta.

---

### 4. Tuplas vs Arrays híbridos
```ts
type Hybrid = [string, ...number[]];
```
Puedes tener un valor fijo seguido de una cantidad indefinida de otro tipo.

> ⚠️ **Error común**: tratarlo como array homogéneo, cuando no lo es.

---

### 5. Tipos más seguros
```ts
function safeAccess<T extends any[], I extends number>(arr: T, index: I): T[I] {
  return arr[index];
}
```
> ⚠️ **Error común**: acceder a posiciones inexistentes sin validación.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Tupla | `[T1, T2]` | `[string, number]` | Agregar más elementos |
| Array | `T[]` | `number[]` | Esperar heterogeneidad |
| Hybrid | `[T, ...U[]]` | `[string, ...number[]]` | Tratar como homogéneo |
| Infer | `infer X` en `[X, ...Y[]]` | `extraer primer tipo` | No validar entrada |
| Safe Access | `T[I]` | obtener por índice | No controlar rangos |

---

## 🧙‍♀️ Moraleja
> *Las tuplas te dan certeza, los arrays libertad. Mezclarlos sin sabiduría es como invocar a dos demonios con un solo círculo de protección.*