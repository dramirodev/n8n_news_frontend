

Los **Conditional Types** permiten expresar tipos que dependen de condiciones en tiempo de tipado. Son la bifurcación lógica de la gramática de tipos: permiten transformar tipos en función de otros, y lo hacen de forma distributiva cuando se aplican sobre uniones.

Su sintaxis es un encantamiento ancestral: `T extends U ? X : Y`

---

## 📚 Temas incluidos y explicación extendida

### 1. Sintaxis básica
```ts
type EsCadena<T> = T extends string ? true : false;
```
> ⚠️ **Error común**: confundirlo con operadores ternarios en tiempo de ejecución.

---

### 2. Distribución
```ts
type SoloCadena<T> = T extends string ? T : never;
type Resultado = SoloCadena<string | number>; // Resultado: string
```
> ⚠️ **Error común**: no entender que se aplica a cada miembro de una unión.

---

### 3. Uso de `infer`
```ts
type Retorno<F> = F extends (...args: any[]) => infer R ? R : never;
```
> ⚠️ **Error común**: no usar `infer` cuando necesitas extraer tipos internos.

---

### 4. Anidamiento y combinación
```ts
type Tipo<T> = T extends string ? 'string' : T extends number ? 'number' : 'otro';
```
> ⚠️ **Error común**: no considerar el orden de las condiciones anidadas.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Básico | `T extends U ? X : Y` | EsCadena | Pensar que es en runtime |
| Distribución | `T extends U` con unión | evalúa cada tipo por separado | Confusión con intersecciones |
| Inferencia | `infer R` | extrae retorno o params | No usar `infer` |
| Anidamiento | `T extends A ? X : T extends B ? Y : Z` | múltiples caminos | No controlar orden |

---

## 🧙‍♀️ Moraleja
> *Un conditional type es un oráculo binario: siempre dice la verdad… si sabes preguntarle bien.*