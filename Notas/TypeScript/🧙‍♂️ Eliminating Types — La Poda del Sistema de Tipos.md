A veces no queremos extender ni extraer... queremos **eliminar**. Y eso es exactamente lo que esta sección enseña: cómo eliminar tipos específicos, propiedades o ramas enteras usando herramientas como `Exclude`, `never`, y condicionales destructivos.

---

## 📚 Temas incluidos y explicación extendida

### 1. Usar `Exclude<T, U>`
```ts
type SinString = Exclude<string | number | boolean, string>; // number | boolean
```
> ⚠️ **Error común**: olvidar que solo elimina tipos *compatibles* con `U`.

---

### 2. Reemplazar por `never`
```ts
type Filtrar<T> = T extends string ? never : T;
```
> ⚠️ **Error común**: no controlar el resultado si todo es eliminado.

---

### 3. Quitar propiedades de objetos
```ts
type SinClave<T, K extends keyof T> = {
  [P in keyof T as P extends K ? never : P]: T[P];
};
```
> ⚠️ **Error común**: no usar `as` con `never` para remover clave.

---

### 4. Anidamiento con exclusión
```ts
type QuitarNulo<T> = T extends null | undefined ? never : T;
```
> ⚠️ **Error común**: olvidar `undefined`, que aparece frecuentemente.

---

## 🧠 Tabla resumen
| Técnica | Resultado | Útil para |
|---------|-----------|-----------|
| `Exclude` | quitar tipos simples | uniones |
| condicional `never` | eliminar dinámico | estructuras complejas |
| `as never` | eliminar propiedades | objetos |

---

## 🧙‍♀️ Moraleja
> *Eliminar tipos es como hacer poda mágica: menos ramas, pero más claridad.*