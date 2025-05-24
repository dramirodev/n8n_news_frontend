 
## Functional Safe Composition Pattern (FSCP)

*"Los aprendices imprudentes se ahogan en `any`. Los sabios construyen fortalezas con `unknown`, vigilan con type guards y protegen su reino con `never`."*

---

## 🧙 Descripción

El **Patrón de la Composición Segura** es una técnica avanzada de arquitectura tipada en TypeScript que busca:
- Aislar al máximo el **caos (`unknown`)**.
- Encapsular y controlar **el veneno (`any`)**.
- Usar **`never` como vigilante del control exhaustivo**.
- Promover una **composición funcional y declarativa**, libre de hechizos oscuros como el casting descontrolado o el duck typing imprudente.

---

## ⚙ Componentes clave del patrón

| Elemento     | Propósito                                    |
|--------------|----------------------------------------------|
| `unknown`     | Primer muro de seguridad ante datos externos. |
| Type Guards   | Refinería quirúrgica, encapsulando `any` solo donde es necesario. |
| `never`       | Guardia exhaustiva que asegura que el dominio nunca tenga ramas sin cubrir. |
| Composición declarativa | Uso de funciones puras y tipos discriminados para manejar datos. |

---

## 🛡 Ejemplo completo

### 1. Definir el dominio claro, puro y sin adornos innecesarios
```typescript
interface CriaturaConNombre {
  tipo: 'criatura';
  nombre: string;
}

interface MensajeError {
  tipo: 'error';
  mensaje: string;
}

type ResultadoAPI = CriaturaConNombre | MensajeError;

```

### **2. Recibir datos inciertos como** **unknown**

```typescript
function recibirDeAPI(): unknown {
  return Math.random() > 0.5
    ? { tipo: 'criatura', nombre: 'Fénix' }
    : { tipo: 'error', mensaje: 'Bestia no encontrada' };
}
```

### **3. Refinar con type guard encapsulando**  **any**

```typescript
function esResultadoAPI(obj: unknown): obj is ResultadoAPI {
  if (typeof obj !== 'object' || obj === null) return false;
  if ('tipo' in obj) {
    const tipo = (obj as any).tipo;
    return tipo === 'criatura' || tipo === 'error';
  }
  return false;
}
```

### **4. Procesar de forma exhaustiva con** **never**

```typescript
function manejarResultado(resultado: ResultadoAPI) {
  switch (resultado.tipo) {
    case 'criatura':
      return `Has encontrado a: ${resultado.nombre}`;
    case 'error':
      return `Error: ${resultado.mensaje}`;
    default:
      return manejarCasoImposible(resultado);
  }
}

function manejarCasoImposible(valor: never): never {
  throw new Error(`Caso imposible detectado: ${JSON.stringify(valor)}`);
}
```

### **5. Componer todo de forma segura y funcional**

```typescript
const respuestaBruta = recibirDeAPI();

if (esResultadoAPI(respuestaBruta)) {
  console.log(manejarResultado(respuestaBruta));
} else {
  console.error('Respuesta inválida de la API.');
}
```

## **🎯 Beneficios**

- **Seguridad de tipos 100%.**
- **any bajo contención quirúrgica.**
- **Exhaustividad garantizada.**
- **Claridad semántica y separación estricta entre capa de entrada, validación y dominio.**
- **Facilidad de escalado y mantenibilidad épica.**


## **🧙‍♂️ Integración con Mónadicos**

  

Una **mónada** es como una **caja mágica tipada que encapsula efectos secundarios, errores o incertidumbres**, permitiéndote componer funciones de manera segura, sin que el error o el caos se propague libremente.

  

#### **Ejemplos famosos de mónadas en TypeScript/FP:**

- Maybe (o Option) → representa algo que puede existir (Some) o no (None).
- Result (o Either) → representa éxito (Ok) o error (Err).
- Task → representa computación asíncrona controlada.
- IO → representa una acción de entrada/salida que puede diferirse.

  

#### **Ejemplo con** 

#### **Result**

```typescript
type Result<T, E> = { ok: true, value: T } | { ok: false, error: E };

function parseJSON(input: string): Result<any, string> {
  try {
    return { ok: true, value: JSON.parse(input) };
  } catch (e) {
    return { ok: false, error: 'JSON inválido' };
  }
}

const resultado = parseJSON('{ "criatura": "Dragón" }');

if (resultado.ok) {
  console.log('Éxito:', resultado.value);
} else {
  console.error('Error:', resultado.error);
}
```
