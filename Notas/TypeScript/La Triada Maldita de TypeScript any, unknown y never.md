Estos tres tipos son como tres arquetipos de magos:

- El temerario (any).
- El paranoico (unknown).
- El nihilista (never).

Veamos quiénes son, cómo operan, y cómo evitar que tu código termine como un portal abierto al Reino del Caos™.

---
### **🟥**  **any** : El hechizo del todo vale**
#### **¿Qué es?**
any es el **“haz lo que quieras”** de TypeScript.
Le dices al compilador:
> _“Relájate, confía en mí, yo sé lo que hago.”_

#### **Características:**

- Puedes asignarle cualquier cosa.
- Puedes acceder a cualquier propiedad o método, incluso si no existe.
- Es como apagar todos los detectores mágicos de seguridad.

```typescript
let bestia: any = 'dragón';
bestia.volar(); // TypeScript no se queja, pero en runtime... BOOM.
```

#### **Cuándo usarlo:**

⚠️ Casi nunca, a menos que estés integrando con código que literalmente **no puedes tipar aún** (como librerías muy dinámicas o APIs legacy horrendas).

---
### **🟩**  **unknown** **: El hechizo prudente**

#### **¿Qué es?**
unknown es como any, pero con cinturón de seguridad y casco reglamentario.
Te permite almacenar cualquier cosa, **pero no hacer nada con ella hasta que la verifiques**.

```typescript
let criatura: unknown = 'fénix';
criatura.volar(); // 💥 Error de compilación.
```

#### **Uso correcto:**

```typescript
if (typeof criatura === 'string') {
  console.log(criatura.toUpperCase()); // ✔️ Seguro ahora.
}
```

#### **Cuándo usarlo:**
- Cuando recibes datos de orígenes inciertos (APIs, inputs del usuario).
- Cuando quieres forzar al desarrollador a ser **explícito** en las comprobaciones de tipo.

---
### **⬛**  **never**  : **El hechizo prohibido que no retorna**

#### **¿Qué es?**
never representa **lo imposible**.
Funciones que **nunca retornan** (porque lanzan errores o loops infinitos).

```typescript

function invocarError(): never {
  throw new Error('¡El grimorio ha explotado!');
}

function cicloEterno(): never {
  while (true) {}
}
```

#### **Cuándo se usa:**
- Funciones que **siempre lanzan errores**.
- **Chequeo exhaustivo** en **switch**:

```typescript
function manejarCriatura(criatura: 'dragón' | 'fénix') {
  switch (criatura) {
    case 'dragón':
      return 'Escupe fuego';
    case 'fénix':
      return 'Renace';
    default:
      const imposible: never = criatura; // Si alguien añade 'grifo', TypeScript explotará aquí.
  }
}
```

---
#### **Utilidad:**

- Asegura que tu código **es exhaustivo y robusto**.
- Te protege contra nuevas variantes no contempladas.
## **🧙‍♂️ Resumen con tono profético:**

| **Tipo** | **Permisividad**   | **Seguridad** | **Uso típico**                        |
| -------- | ------------------ | ------------- | ------------------------------------- |
| any      | Absurda            | Nula          | Prototipado rápido, legacy APIs       |
| unknown  | Alta (con chequeo) | Alta          | Datos externos, inputs inseguros      |
| never    | Imposible          | Absoluta      | Funciones que nunca deberían retornar |
