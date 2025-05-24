

`infer` es el cuchillo quirúrgico del sistema de tipos de TypeScript. Permite **extraer tipos ocultos** desde dentro de estructuras complejas cuando se utiliza en tipos condicionales. Esta sección profundiza en patrones avanzados que desbloquean su verdadero poder.

---

## 📚 Temas incluidos y explicación extendida

### 1. Extraer tipo de retorno
```ts
type Retorno<F> = F extends (...args: any[]) => infer R ? R : never;
```
> ⚠️ **Error común**: no usar `infer` y duplicar lógica con overloading.

---

### 2. Extraer tipo de argumentos
```ts
type Argumentos<F> = F extends (...args: infer A) => any ? A : never;
```
> ⚠️ **Error común**: no usar tupla en la extracción.

---

### 3. Extraer tipo de elementos de array
```ts
type Elemento<A> = A extends (infer T)[] ? T : never;
```
> ⚠️ **Error común**: no validar si realmente es array.

---

### 4. Extraer parte interna de estructura anidada
```ts
type Interno<T> = T extends Promise<infer P> ? P : never;
```
> ⚠️ **Error común**: asumir que todo es `Promise<T>` sin fallback.

---

### 5. Descomponer tuplas y objetos
```ts
type Cabecera<T> = T extends [infer H, ...any[]] ? H : never;
```
> ⚠️ **Error común**: no considerar tuplas vacías.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Return type | `infer R` | `(...args) => R` | No usar infer |
| Args | `infer A[]` | extrae tupla de args | Tratar como `any[]` |
| Elemento | `A extends (infer T)[]` | Array → tipo interno | No validar array |
| Promise | `Promise<infer T>` | desempaquetar | No controlar fallback |
| Tupla | `[infer H, ...rest]` | acceder primer valor | Ignorar edge cases |

---

## 🧙‍♀️ Moraleja
> *Infer es como una lupa mágica: revela lo que los tipos ocultan. Pero cuidado: si apuntas mal, sólo verás el reflejo de tu error.*