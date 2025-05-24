Cuando lidias con uniones de tipos, a veces necesitas **extraer** solo las partes que te interesan: funciones, objetos, strings, lo que sea. TypeScript nos da herramientas para filtrar, reducir y transformar estas uniones.

---

## 📚 Temas incluidos y explicación extendida

### 1. `Extract<T, U>`
Extrae los miembros de `T` que son asignables a `U`.
```ts
type SoloNumeros = Extract<string | number | boolean, number>; // number
```
> ⚠️ **Error común**: creer que `Extract` transforma, cuando solo filtra.

---

### 2. `Exclude<T, U>`
Remueve los miembros de `T` que son asignables a `U`.
```ts
type SinBooleanos = Exclude<string | number | boolean, boolean>; // string | number
```

---

### 3. Personalizado con condicional
```ts
type SoloObjetos<T> = T extends object ? T : never;
```
> ⚠️ **Error común**: olvidar que `function` también es `object` en TS.

---

### 4. Filtrar por propiedades
```ts
type TieneNombre<T> = T extends { nombre: any } ? T : never;
```
> ⚠️ **Error común**: no usar condicional distributivo sobre uniones.

---

## 🧠 Tabla resumen
| Herramienta | Acción | Nota |
|-------------|--------|------|
| Extract | Mantiene miembros compatibles | Filtro |
| Exclude | Elimina miembros compatibles | Reducción |
| `T extends ?` | Distribuye condicionalmente | Evaluación individual |

---

## 🧙‍♀️ Moraleja
> *Extraer tipos de una unión es como separar pociones por color: requiere precisión, o terminarás bebiendo veneno.*