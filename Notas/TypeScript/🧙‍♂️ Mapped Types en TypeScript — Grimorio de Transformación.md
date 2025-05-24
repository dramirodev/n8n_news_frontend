Los **Mapped Types** son uno de los artefactos más poderosos de TypeScript. Permiten crear nuevos tipos a partir de otros, mapeando sus propiedades y transformándolas una por una. Si alguna vez quisiste modificar todas las propiedades de un objeto a `readonly`, `optional`, o `null`, entonces ya sentiste su poder.

---

## 📚 Temas incluidos y explicación extendida

### 1. Cómo funcionan los Mapped Types
Un Mapped Type recorre las claves de un tipo usando `keyof` y transforma cada propiedad:

```ts
type ReadonlyTodo<T> = {
  readonly [K in keyof T]: T[K];
};
```

> ⚠️ **Error común**: creer que `[K in keyof T]` es lo mismo que iterar en tiempo de ejecución. Aquí hablamos del nivel tipo.

---

### 2. Modificadores: `readonly`, `?` (opcional) y `-` para removerlos
Puedes añadir o eliminar modificadores como `readonly` u `optional`:

```ts
type Optional<T> = {
  [K in keyof T]?: T[K];
};

type Mutable<T> = {
  -readonly [K in keyof T]: T[K];
};
```

> ⚠️ **Error común**: olvidar el `-` y pensar que `readonly` se puede sobrescribir mágicamente.

---

### 3. Combinando Mapped Types con Condicionales
Puedes transformar propiedades condicionalmente:

```ts
type NullableProps<T> = {
  [K in keyof T]: T[K] extends string ? string | null : T[K];
};
```

> ⚠️ **Error común**: no controlar las ramas condicionales, lo que puede causar tipos no esperados.

---

### 4. Key remapping (renombrar claves)

```ts
type PrefixKeys<T> = {
  [K in keyof T as `prefixed_${string & K}`]: T[K];
};
```

> ⚠️ **Error común**: usar `as` sin entender que cambia completamente la clave.

---

### 5. Unión entre Mapped y Union Types
Puedes usar Mapped Types para iterar sobre una unión de literales:

```ts
type Flags = {
  [K in 'read' | 'write' | 'delete']: boolean;
};
```

> ⚠️ **Error común**: asumir que esto itera sobre un array real. Es una transformación puramente estática.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Mapeo simple | `[K in keyof T]` | Copiar propiedades | Creer que es un loop real |
| Modificadores | `readonly`, `?`, `-readonly` | Añadir/quitar flags | Olvidar `-` |
| Condicionales | `T[K] extends ...` | Propiedades según su tipo | Tipos imprecisos |
| Remapeo de clave | `as NewKey` | Renombrar propiedades | Claves inesperadas |

---

## 🧙‍♀️ Moraleja
> *Los Mapped Types son como encantamientos de transformación: aplican una regla sobre todas las propiedades de un objeto. Úsalos para crear artefactos más seguros, no para convertir tu sistema de tipos en una hidra inmutable.*
