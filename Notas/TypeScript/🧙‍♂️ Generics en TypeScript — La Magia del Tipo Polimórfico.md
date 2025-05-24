

Los **Generics** son los grimorios del mundo de TypeScript: permiten escribir funciones, tipos y clases que funcionan con múltiples formas sin perder precisión ni seguridad. En vez de escribir diez veces la misma función para cada tipo, escribes una vez con un tipo genérico que se adapta.

El símbolo del mago en este caso es `<T>`, pero no te dejes engañar por su modestia visual.

---

## 📚 Temas incluidos y explicación extendida

### 1. Genéricos simples
```ts
function identidad<T>(valor: T): T {
  return valor;
}
```
> ⚠️ **Error común**: no usar `T`, y caer en el abismo de `any`.

---

### 2. Constraints (restricciones)
```ts
function logLongitud<T extends { length: number }>(x: T) {
  console.log(x.length);
}
```
> ⚠️ **Error común**: asumir que `T` siempre tiene propiedades.

---

### 3. Default types (valores por defecto)
```ts
type Resultado<T = string> = T;
```
> ⚠️ **Error común**: no usarlos y complicar firmas simples.

---

### 4. Múltiples parámetros genéricos
```ts
function mezclar<T, U>(a: T, b: U): [T, U] {
  return [a, b];
}
```
> ⚠️ **Error común**: tratar de hacer todo con un solo `T` universal.

---

### 5. Genéricos condicionales
```ts
type Nullable<T> = T extends undefined ? never : T | null;
```
> ⚠️ **Error común**: olvidar que también se pueden combinar con tipos condicionales.

---

### 6. Infer dentro de Genéricos
```ts
type Retorno<F> = F extends (...args: any[]) => infer R ? R : never;
```
> ⚠️ **Error común**: no usar `infer` y duplicar lógicas internas.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Generic simple | `<T>` | `identidad<T>(v: T)` | Usar `any` |
| Constraint | `<T extends X>` | `T extends { length: number }` | Asumir propiedades |
| Default | `<T = X>` | `Resultado<T = string>` | No declarar por defecto |
| Múltiples genéricos | `<T, U>` | `[T, U]` | Usar solo T |
| Infer | `infer X` | `Retorno<F>` | No extraer retorno |

---

## 🧙‍♀️ Moraleja
> *Los generics son como hechizos con parámetros: más potentes mientras más los entiendes, pero peligrosos si los repites sin saber qué significan.*