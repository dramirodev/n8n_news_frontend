

**Type Inference** es el arte de dejar que TypeScript adivine lo que tú ya sabes. Gracias a su sistema de inferencia, muchas veces no necesitas anotar tipos manualmente.

Pero el verdadero dominio surge al **entender cuándo infiere, cómo lo hace y cómo puedes guiarlo sin estorbarlo**.

---

## 📚 Temas incluidos y explicación extendida

### 1. Inferencia directa
```ts
let x = 5; // number
const saludo = 'hola'; // "hola"
```
> ⚠️ **Error común**: asumir que `const` y `let` infieren igual.

---

### 2. Contextual inference (param vs retorno)
```ts
const sumar = (a: number, b: number) => a + b; // retorno inferido
```
> ⚠️ **Error común**: olvidar tipos en parámetros, y perder precisión.

---

### 3. Inferencia con funciones genéricas
```ts
function identidad<T>(valor: T): T {
  return valor;
}
const x = identidad(42); // T = number
```
> ⚠️ **Error común**: declarar `<T>` sin usarlo correctamente.

---

### 4. Inferencia inversa y tuplas
```ts
function primero<T extends any[]>(lista: T): T[0] {
  return lista[0];
}
```
> ⚠️ **Error común**: usar `T[]` en lugar de `T extends any[]`

---

## 🧠 Tabla resumen
| Contexto | Inferencia | Precisión |
|----------|------------|-----------|
| let x = 3 | number | estándar |
| const y = 'x' | 'x' (literal) | exacta |
| Función genérica | `T` inferido | adaptable |
| Parámetros sin tipo | `any` implícito | error silencioso |

---

## 🧙‍♀️ Moraleja
> *Dejar que el compilador infiera sin saber qué está infiriendo… es como dejarle a un dragón decidir tu ruta sin mapa.*