

Los **Type Predicates Avanzados** son funciones mágicas que enseñan a TypeScript lo que ya sabes tú en tiempo de ejecución. No solo son para `typeof`, sino que pueden refinar tipos complejos, clases, estructuras y jerarquías con precisión quirúrgica.

---

## 📚 Temas incluidos y explicación extendida

### 1. Guardias personalizados
```ts
function esUsuario(val: unknown): val is { nombre: string } {
  return typeof val === 'object' && val !== null && 'nombre' in val;
}
```
> ⚠️ **Error común**: no verificar null/undefined en objetos.

---

### 2. Guardias de tipo marca (branded)
```ts
type ID = string & { __brand: 'ID' };
function esID(valor: unknown): valor is ID {
  return typeof valor === 'string'; // y validación adicional
}
```
> ⚠️ **Error común**: asumir que `as` añade marcas mágicamente.

---

### 3. Type guards dentro de clases
```ts
class ErrorConMensaje {
  constructor(public mensaje: string) {}
}

function esErrorConMensaje(x: unknown): x is ErrorConMensaje {
  return x instanceof ErrorConMensaje;
}
```
> ⚠️ **Error común**: usar typeof en instancias.

---

### 4. Assertion functions con `asserts`
```ts
function assertEsString(x: unknown): asserts x is string {
  if (typeof x !== 'string') throw new Error('No es string');
}
```
> ⚠️ **Error común**: no usar el tipo refinado tras la aserción.

---

## 🧠 Tabla resumen
| Tipo | Ejemplo | Dónde usarlo | Error común |
|------|---------|--------------|-------------|
| Simple predicate | `x is T` | filtros, if | olvidar `is` |
| Branded | `T & { __brand: 'X' }` | validaciones | asumir marca por as |
| instanceof | clases | jerarquías OO | usar typeof |
| asserts | `asserts x is T` | throws/checks | seguir sin refinar |

---

## 🧙‍♀️ Moraleja
> *Un type predicate bien usado transforma al compilador de policía en aliado.*