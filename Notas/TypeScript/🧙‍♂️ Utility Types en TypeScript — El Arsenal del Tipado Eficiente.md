

TypeScript provee una serie de **tipos utilitarios integrados** que permiten transformar, extender y restringir tipos de forma expresiva y segura.

Son como herramientas mágicas listas para ser invocadas: `Partial`, `Required`, `Pick`, `Omit`, `Record`, `Exclude`, `Extract`, `ReturnType`, y otros tantos.

---

## 📚 Temas incluidos y explicación extendida

### 1. `Partial<T>`
Convierte todas las propiedades de `T` en opcionales.
```ts
Partial<{ a: number; b: string }> // { a?: number; b?: string }
```

---

### 2. `Required<T>`
Convierte todas las propiedades en requeridas.
```ts
Required<{ a?: number }> // { a: number }
```

---

### 3. `Readonly<T>`
Hace todas las propiedades de T inmutables.
```ts
Readonly<{ a: number }> // { readonly a: number }
```

---

### 4. `Pick<T, K>`
Extrae un subconjunto de propiedades.
```ts
Pick<{ a: number; b: string }, 'a'> // { a: number }
```

---

### 5. `Omit<T, K>`
Elimina un subconjunto de propiedades.
```ts
Omit<{ a: number; b: string }, 'b'> // { a: number }
```

---

### 6. `Record<K, T>`
Construye un objeto con claves K de tipo T.
```ts
Record<'id' | 'nombre', string> // { id: string; nombre: string }
```

---

### 7. `Exclude<T, U>`
Remueve de T los tipos asignables a U.
```ts
Exclude<'a' | 'b' | 'c', 'a'> // 'b' | 'c'
```

---

### 8. `Extract<T, U>`
Extrae de T los tipos asignables a U.
```ts
Extract<string | number, number> // number
```

---

### 9. `ReturnType<T>`
Extrae el tipo de retorno de una función.
```ts
ReturnType<() => number> // number
```

---

## 🧠 Tabla resumen
| Tipo | Propósito | Error común |
|------|-----------|-------------|
| Partial | Vuelve opcionales | Olvidar que afecta todos los campos |
| Required | Fuerza obligatoriedad | Sobre tipos ya no opcionales |
| Readonly | Inmutable | Intentar reasignar |
| Pick | Extrae propiedades | Claves inexistentes |
| Omit | Elimina claves | Usar con clave que no existe |
| Record | Crea objetos | Usar clave que no sea string/number |
| Exclude | Quita tipos | No usar `as` al evaluar |
| Extract | Filtra por asignabilidad | No matchear correctamente |
| ReturnType | Saca retorno | No usar con tipo no función |

---

## 🧙‍♀️ Moraleja
> *Los Utility Types son los atajos de un verdadero maestro: invócalos con intención, no por moda.*