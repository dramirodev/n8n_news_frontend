

## 1. Understanding Conditional Type Structures

Los tipos condicionales son como sentencias `if` para tipos:

```typescript
type EsCadena<T> = T extends string ? 'Sí' : 'No';
```

Esto se lee como:  
Si `T` es compatible con `string`, entonces devuelve `'Sí'`, si no `'No'`.

**Error común:**  
Olvidar que `extends` en este contexto es más una comparación de compatibilidad, no herencia directa.

---

## 2. The `extends` Operator Explained

Aquí `extends` actúa como el vigilante del gremio:

```typescript
type EsNumero<T> = T extends number ? 'Sí' : 'No';
```

Evalúa si un tipo "se comporta como" el otro, no si es estrictamente igual.

**Error común:**  
Pensar que `extends` fuerza a que `T` sea exactamente igual a `number`.

---

## 3. Constraining Type Parameters in Generics

Cuando haces funciones genéricas, puedes imponer que solo acepten tipos concretos:

```typescript
function procesar<T extends string>(valor: T) { }
```

**Error común:**  
No imponer restricciones y acabar con funciones que aceptan cualquier cosa.

---

## 4. Complex Conditional Types

Tipos condicionales dentro de tipos condicionales:

```typescript
type Validar<T> = T extends string | number ? 'Válido' : 'Inválido';
```

**Error común:**  
Abusar y crear árboles de tipos imposibles de leer.

---

## 5. Advanced Pattern Matching with Conditional Types

Gracias a `infer`, puedes capturar partes de tipos:

```typescript
type ExtraerElemento<T> = T extends (infer U)[] ? U : T;
```

**Error común:**  
No usar `infer` y acabar repitiendo tipos manualmente.

---

## 6. Understanding Type Inference

TypeScript puede inferir tipos mágicamente dentro de tipos condicionales:

```typescript
type Inferencia<T> = T extends infer U ? U : never;
```

**Error común:**  
Creer que `infer` solo sirve en funciones.

---

## 7. Advanced Tuple Inferencing

Puedes diseccionar tuplas:

```typescript
type PrimerElemento<T> = T extends [infer U, ...any[]] ? U : never;
```

**Error común:**  
Confundir tuplas con arrays simples.

---

## 8. Type Extraction from Functions with `infer`

Puedes extraer el tipo de retorno de una función:

```typescript
type Retorno<F> = F extends (...args: any[]) => infer R ? R : never;
```

**Error común:**  
No usar `infer` en tipos de funciones.

---

## 9. Advanced Inference in Custom Generic Types

Puedes crear tipos genéricos que extraen parámetros de funciones:

```typescript
type Parametros<T> = T extends (...args: infer U) => any ? U : never;
```

**Error común:**  
Olvidar que puedes capturar listas enteras de argumentos.

---

# Tabla de Tipos Condicionales estilo grimorio gótico

|N°|Concepto|Sintaxis|Ejemplo|Error Típico|
|---|---|---|---|---|
|1|Tipo Condicional Básico|`T extends X ? A : B`|`EsCadena<string>` → `'Sí'`|Creer que es una comparación exacta.|
|2|Uso de `extends` en tipos|`T extends number ? ... : ...`|`EsNumero<123>` → `'Sí'`|Pensar que solo evalúa igualdad exacta.|
|3|Restricción en genéricos|`function f<T extends X>() {}`|Solo acepta `string` si pones `T extends string`|Olvidar limitar, aceptando cualquier cosa.|
|4|Tipos condicionales complejos|Anidación de tipos condicionales|`Validar<true>` → `'Inválido'`|Nidos infernales de tipos ilegibles.|
|5|Pattern matching avanzado (`infer`)|`T extends (infer U)[] ? U : T`|`ExtraerElemento<string[]>` → `string`|Repetición manual de tipos sin `infer`.|
|6|Inferencia básica con `infer`|`T extends infer U ? U : never`|`Inferencia<number>` → `number`|Pensar que no sirve para nada (spoiler: sí).|
|7|Inferencia de tuplas|`T extends [infer U, ...any[]] ? U : never`|`PrimerElemento<[1,2,3]>` → `1`|Tratar tuplas como arrays comunes.|
|8|Extracción de retorno de funciones con `infer`|`F extends (...args: any[]) => infer R ? R : never`|`Retorno<() => string>` → `string`|No usarlo y casarte con tipos fijos.|
|9|Inferencia avanzada de parámetros de funciones|`F extends (...args: infer U) => any ? U : never`|`Parametros<(a: string, b: number) => void>` → `[string, number]`|No capturar argumentos como grupo.|

---

# Árbol inferencial de Tipos Condicionales (versión ASCII surrealista)

```
          ┌──────────────────────────────────┐
          │     Tipo Condicional Básico      │
          └──────────────┬───────────────────┘
                         │
             ┌───────────┴───────────┐
             │                       │
  Uso de extends              Inferencia con infer
             │                       │
   ┌────────┴───────┐         ┌─────┴─────────┐
   │                │         │               │
Restricción     Pattern   Inferencia    Extraer Retorno
 en genéricos  Matching    de Tuplas      de Función
   │
   └────────────────────────┐
                            │
        Tipos Condicionales Complejos
                            │
               ┌────────────┴────────────┐
               │                         │
 Inferencia avanzada   Inferencia avanzada
en tipos genéricos    de parámetros
```

## Moraleja

Los tipos condicionales en TypeScript son como pociones arcanas: potentes, pero peligrosas si no sabes lo que haces. Úsalos con elegancia, no con exceso.

---