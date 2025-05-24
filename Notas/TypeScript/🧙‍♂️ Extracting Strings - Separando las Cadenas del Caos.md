

En TypeScript podemos **extraer partes de strings** definidos como tipos usando `infer` en los Template Literal Types. Esta técnica es útil para validar patrones, manipular rutas y construir sistemas de análisis de strings tipados.

---

## 📚 Temas incluidos y explicación extendida

### 1. Extraer fragmentos con `infer`
```ts
type ExtraerRuta<T> = T extends `GET ${infer R}` ? R : never;
type Ruta = ExtraerRuta<'GET /usuario'>; // '/usuario'
```

### 2. Extraer múltiples partes
```ts
type Fragmentar<T> = T extends `${infer A}-${infer B}` ? [A, B] : never;
type Resultado = Fragmentar<'user-id'>; // ['user', 'id']
```

### 3. Extraer con delimitadores
```ts
type Dominio<T> = T extends `${infer U}@${string}` ? U : never;
type UsuarioEmail = Dominio<'juan@example.com'>; // 'juan'
```

---

## 🧠 Tabla resumen
| Patrón | Ejemplo | Resultado |
|--------|---------|-----------|
| `${infer A}` | `Hola ${A}` | 'Hola' extraído |
| `${infer A}-${infer B}` | 'x-y' | ['x','y'] |
| delimitado | 'x@y' | 'x' |

---

## 🧙‍♀️ Moraleja
> *Los tipos string pueden ser diseccionados como pergaminos mágicos… si usas la cuchilla de `infer` con destreza.*
