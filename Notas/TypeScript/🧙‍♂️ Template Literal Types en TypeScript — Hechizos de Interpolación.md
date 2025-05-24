
Los **Template Literal Types** en TypeScript permiten construir tipos de texto dinámicos combinando cadenas, literales y tipos inferidos. Son la versión mágica de los `string templates` de JavaScript, pero funcionando en el plano espectral del sistema de tipos.

Son extremadamente útiles para:
- Generar tipos como `'GET /user' | 'POST /user'`
- Validar que una cadena tenga un formato específico
- Crear alias tipados automáticos

---

## 📚 Temas incluidos y explicación extendida

### 1. Template Literal básico
Permite concatenar tipos string:
```ts
type Endpoint = `GET /${string}`;
```
> ⚠️ **Error común**: pensar que esto crea valores en tiempo de ejecución. No, esto es solo a nivel tipo.

---

### 2. Interpolación de literales
```ts
type NombreUsuario = `usuario_${number}`;
```
Puedes interpolar literales como `string`, `number`, `boolean`.

> ⚠️ **Error común**: no restringir el tipo interpolado y obtener combinaciones absurdas.

---

### 3. Unión de templates
Puedes usar uniones dentro del template:
```ts
type Métodos = 'GET' | 'POST';
type Rutas = '/home' | '/login';
type Combinaciones = `${Métodos} ${Rutas}`;
```

> ⚠️ **Error común**: no entender que esto genera la combinación de todas las posibilidades.

---

### 4. Inferencia en patrones de templates
```ts
type ExtraerRuta<T> = T extends `${infer Metodo} ${infer Ruta}` ? Ruta : never;
type Resultado = ExtraerRuta<'GET /login'>; // '/login'
```

> ⚠️ **Error común**: olvidar que `infer` funciona dentro de los templates.

---

### 5. Transformaciones avanzadas
```ts
type Capitalizar<T extends string> = T extends `${infer F}${infer R}` ? `${Uppercase<F>}${R}` : T;
```

> ⚠️ **Error común**: subestimar el poder de combinar templates con `infer` y `Uppercase`/`Lowercase`.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Ejemplo | Error común |
|---|---|---|---|
| Concatenación | \`a_${string}\` | GET /${string} | Creer que es runtime |
| Unión + template | \`${Métodos} ${Rutas}\` | 'GET /home' | No controlar combinaciones |
| Inferencia | T extends \`${infer A}_${infer B}\` | Extraer segmentos | Olvidar infer en template |
| Capitalización | `${Uppercase<F>}` | Transformar claves | Usar fuera de string |

---

## 🧙‍♀️ Moraleja
> *Los template literal types son como portales interdimensionales entre cadenas y tipos. Si los abres sin cuidado, podrías invocar combinaciones que ni tu compilador querrá tocar.*
