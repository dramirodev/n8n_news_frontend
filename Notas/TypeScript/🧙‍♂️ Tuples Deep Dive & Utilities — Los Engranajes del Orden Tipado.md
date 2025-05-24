

Las **tuplas** son estructuras ordenadas que representan secuencias heterogéneas. En este capítulo, exploramos sus límites, combinaciones con utilidades y secretos de manipulación avanzada.

---

## 📚 Temas incluidos y explicación extendida

### 1. Longitud fija vs extensible
```ts
type Fija = [string, number];
type Extensible = [string, ...number[]];
```
> ⚠️ **Error común**: asumir que ambas pueden ser usadas igual.

---

### 2. Acceso por índice
```ts
type T = [string, number];
type Segundo = T[1];
```
> ⚠️ **Error común**: acceder a índice fuera de rango.

---

### 3. Validar longitud
```ts
type Tiene3<T extends any[]> = T['length'] extends 3 ? true : false;
```
> ⚠️ **Error común**: comparar `length` sin bounds.

---

### 4. Operaciones con utilidades
```ts
type Primera<T extends any[]> = T extends [infer A, ...any[]] ? A : never;
```
> ⚠️ **Error común**: confundir tuplas con arrays normales.

---

### 5. Map, Filter, Reduce en tipos
```ts
type Duplicar<T extends any[]> = {
  [K in keyof T]: [T[K], T[K]];
};
```
> ⚠️ **Error común**: perder los índices clave de mapeo.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Tupla fija | `[A, B]` | heterogénea | Tratar como array |
| Extendida | `[A, ...B[]]` | híbrida | Olvidar que no es homogénea |
| Infer | `[infer X, ...]` | extraer | Usar con array plano |
| Reduce | recursivo | acumula tipo | No usar condicional |
| Validar largo | `T['length']` | 3 = validado | Comparar con valores imposibles |

---

## 🧙‍♀️ Moraleja
> *Las tuplas son como conjuros con componentes precisos: cambia uno y todo el hechizo puede fallar.*