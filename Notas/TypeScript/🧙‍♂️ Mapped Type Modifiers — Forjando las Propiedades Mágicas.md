
En TypeScript, los **modificadores en tipos mapeados** (`+` y `-`) permiten ajustar propiedades: volverlas `readonly`, opcionales (`?`) o eliminar dichos modificadores.

Estas runas de modificación son esenciales para construir transformaciones finas sobre estructuras existentes.

---

## 📚 Temas incluidos y explicación extendida

### 1. `readonly` y `?` en mapeo
```ts
type ReadonlyOpt<T> = {
  readonly [K in keyof T]?: T[K];
};
```
> ⚠️ **Error común**: olvidar aplicar el modificador directamente en la clave.

---

### 2. Eliminar `readonly` y `?`
```ts
type Mutable<T> = {
  -readonly [K in keyof T]: T[K];
};

type Required<T> = {
  -? [K in keyof T]: T[K];
};
```
> ⚠️ **Error común**: no usar `-` para revertir modificadores implícitos.

---

### 3. Combinar modificadores
```ts
type Clean<T> = {
  -readonly -? [K in keyof T]: T[K];
};
```
> ⚠️ **Error común**: aplicar `+` innecesariamente (es por defecto).

---

## 🧠 Tabla resumen
| Sintaxis | Significado | Nota |
|----------|-------------|------|
| `readonly` | Hace la propiedad inmutable | Añade `readonly` |
| `?` | Hace la propiedad opcional | Añade `?` |
| `-readonly` | Quita inmutabilidad | Devuelve a mutable |
| `-?` | Quita opcionalidad | La vuelve requerida |

---

## 🧙‍♀️ Moraleja
> *Dominar los modificadores mapeados es como tener acceso al cincel de los tipos: puedes esculpir estructuras a tu voluntad.*