Una de las habilidades más útiles de los tipos condicionales es la **extracción del tipo de retorno de una función**. Con `infer`, podemos analizar cualquier función y obtener el tipo de lo que devuelve.

Este patrón es tan común que TypeScript lo incluye como tipo built-in: `ReturnType<T>`.

Pero aquí no usamos lo fácil: lo reconstruimos desde cero.

---

## 📚 Temas incluidos y explicación extendida

### 1. Extraer retorno básico
```ts
type Retorno<T> = T extends (...args: any[]) => infer R ? R : never;
```
> ⚠️ **Error común**: usar `T()` o `T[]` en lugar de `T extends (...args)`

---

### 2. Aplicación a funciones genéricas
```ts
function identidad<T>(x: T): T {
  return x;
}
type R = Retorno<typeof identidad>; // T inferido como unknown
```
> ⚠️ **Error común**: esperar que `T` se propague fuera

---

### 3. Aplicación a funciones con overload
```ts
function convertir(x: number): string;
function convertir(x: string): number;
function convertir(x: any): any { return x; }

type R = Retorno<typeof convertir>; // resultado más amplio
```

---

## 🧠 Tabla resumen
| Caso | Resultado | Nota |
|------|-----------|------|
| Función normal | tipo de retorno | ✅ |
| Genérica | `unknown` | ❗ |
| Overload | unión o `any` | ⚠️ cuidado |

---

## 🧙‍♀️ Moraleja
> *Inferir retornos es mirar al futuro con ojos del compilador. Pero cuidado: a veces devuelve visiones borrosas.*