
Cuando los tipos condicionales se combinan con `infer`, mapeo distribuido y otras estructuras, se convierten en un lenguaje de transformación poderosísimo dentro de TypeScript.

Aquí forjamos tipos que **se adaptan, filtran, transforman, o incluso desaparecen** según condiciones.

---

## 📚 Temas incluidos y explicación extendida

### 1. `infer` y condicionales anidados
```ts
type PrimerArgumento<T> = T extends (a: infer A, ...args: any[]) => any ? A : never;
```
> ⚠️ **Error común**: mal uso de posiciones en tuplas o funciones.

---

### 2. Tipos recursivos
```ts
type Desenrollar<T> = T extends Promise<infer U> ? Desenrollar<U> : T;
```
> ⚠️ **Error común**: no poner condición de parada.

---

### 3. Eliminar tipos
```ts
type QuitarNulo<T> = T extends null | undefined ? never : T;
```
> ⚠️ **Error común**: no controlar fallback (cuando todo desaparece).

---

### 4. Evaluación distribuida sobre uniones
```ts
type CadenaUnica<T> = T extends string ? T : never;
```
> ⚠️ **Error común**: no entender que cada miembro se evalúa individualmente.

---

### 5. Filtros avanzados
```ts
type SoloClavesDeTipo<T, U> = {
  [K in keyof T as T[K] extends U ? K : never]: T[K];
};
```
> ⚠️ **Error común**: intentar combinar con `Pick` directamente sin `as`.

---

## 🧠 Tabla resumen
| Patrón | Ejemplo | Propósito |
|--------|---------|-----------|
| infer argumento | `infer A` | extraer de función |
| recursión | `Desenrollar` | promesas, arrays |
| filtrado | `extends tipo ? T : never` | tipo limpieza |
| remapeo clave | `as` | construir nuevos objetos |

---

## 🧙‍♀️ Moraleja
> *Un tipo condicional avanzado es como un acertijo arcano: solo se resuelve si lo lees con el ojo interior del compilador.*