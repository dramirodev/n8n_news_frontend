

Los **Type Predicates** son funciones que, con el poder de la lógica, **afinan los tipos en tiempo de ejecución**. Permiten a TypeScript deducir qué tipo exacto tiene un valor dentro de una unión, basándose en condiciones personalizadas.

Con ellos, los `if` dejan de ser simples barreras y se convierten en hechizos que revelan la verdadera naturaleza de los valores.

---

## 📚 Temas incluidos y explicación extendida

### 1. Sintaxis básica de un Type Predicate
```ts
function esString(valor: unknown): valor is string {
  return typeof valor === 'string';
}
```
> ⚠️ **Error común**: olvidar `valor is string` y perder la inferencia mágica.

---

### 2. Narrowing con predicados
```ts
function manejar(valor: string | number) {
  if (esString(valor)) {
    valor.toUpperCase(); // Es string aquí
  }
}
```
> ⚠️ **Error común**: no aprovechar el narrowing en la rama `if`.

---

### 3. Predicados personalizados complejos
```ts
function esUsuario(x: any): x is { nombre: string } {
  return x && typeof x.nombre === 'string';
}
```
> ⚠️ **Error común**: asumir que `x` no es `null` o `undefined` sin verificar.

---

### 4. Uso con Arrays y filtros
```ts
function esNumero(x: unknown): x is number {
  return typeof x === 'number';
}

const mezcla: unknown[] = [1, 'a', true];
const numeros = mezcla.filter(esNumero); // number[]
```
> ⚠️ **Error común**: olvidar que `.filter` también entiende type guards.

---

### 5. Con clases y jerarquías
```ts
class Perro {}
class Gato {}

function esPerro(pet: Perro | Gato): pet is Perro {
  return pet instanceof Perro;
}
```
> ⚠️ **Error común**: usar `typeof` para clases. Usa `instanceof`.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Type Predicate | `x is T` | `valor is string` | No usar `is` |
| Narrowing | `if (x is T)` | usar tipo específico | No aprovechar el tipo dentro |
| Filtros | `.filter(func)` | `filter(esNumero)` | Asumir `unknown[]` |
| Clases | `instanceof` | `x instanceof C` | Usar `typeof` mal |

---

## 🧙‍♀️ Moraleja
> *Un type predicate es el oráculo del compilador: le permite ver lo que tú ya sabes. No lo subestimes: sin él, TypeScript es como un mago con los ojos vendados.*