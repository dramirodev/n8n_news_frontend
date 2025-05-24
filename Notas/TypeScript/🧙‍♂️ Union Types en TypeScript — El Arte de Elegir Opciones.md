
En el universo encantado de TypeScript, los **Union Types** (`A | B`) son el equivalente a una bifurcación en el camino: permiten que un valor pueda ser de uno u otro tipo. Son extremadamente poderosos para representar **estados finitos**, **variaciones controladas**, y evitar estructuras demasiado genéricas o caóticas.

---

## 📚 Temas incluidos y explicación extendida

### 1. ¿Qué es una unión?
Una unión permite declarar que un tipo puede ser **uno entre varios**.
```ts
type Estado = 'iniciado' | 'cargando' | 'completado';
```
> ⚠️ **Error común**: usar `string` en vez de restringir con un union literal.

---

### 2. El efecto de distribución
Los tipos condicionales se **distribuyen** sobre uniones:
```ts
type SoloCadena<T> = T extends string ? T : never;
type Resultado = SoloCadena<string | number>; // string
```
> ⚠️ **Error común**: no saber que `extends` aplica a cada miembro individual.

---

### 3. Narrowing de uniones
Puedes refinar una unión en tiempo de ejecución usando condiciones:
```ts
function manejar(estado: 'on' | 'off') {
  if (estado === 'on') {
    // estado es 'on'
  } else {
    // estado es 'off'
  }
}
```
> ⚠️ **Error común**: no usar `if`, `switch`, o `in` para discriminar.

---

### 4. Filtrado de uniones
Puedes eliminar tipos no deseados:
```ts
type Limpiar<T> = Exclude<T, null | undefined>;
type Resultado = Limpiar<string | null>; // string
```
> ⚠️ **Error común**: olvidar `Exclude` y construir todo a mano.

---

### 5. Transformaciones
Puedes mapear una unión a otra forma:
```ts
type Capitalizar<T> = T extends string ? Capitalize<T> : T;
type Resultado = Capitalizar<'hola' | 42>; // 'Hola' | 42
```
> ⚠️ **Error común**: asumir que todo comportamiento es homogéneo en una unión.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Unión | `A | B` | `'a' | 'b'` | Usar `string` genérico |
| Distribución | `T extends ...` | `string | number → evalúa a dos tipos` | No entender la separación |
| Narrowing | condicional `if` | verificar `typeof` o `===` | No discriminar correctamente |
| Excluir | `Exclude<T, X>` | `string | null → string` | Filtrar a mano |
| Transformación | `T extends U ? X : Y` | `Capitalizar` sobre strings | No entender que se aplica por elemento |

---

## 🧙‍♀️ Moraleja
> *Los Union Types son como menús en una taberna de tipos: múltiples opciones, pero no puedes pedir todas a la vez. Saber elegir, refinar y transformar es lo que distingue al dev sabio del programador famélico de `any`.*
