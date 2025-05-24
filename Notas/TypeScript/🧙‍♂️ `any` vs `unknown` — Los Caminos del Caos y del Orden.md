En TypeScript, `any` y `unknown` parecen primos, pero son en realidad opuestos filosóficos:

- `any` representa la **libertad absoluta**, a costa de perder toda ayuda del compilador.
- `unknown` representa la **seguridad total**, forzando validación antes de usar.

---

## 📚 Temas incluidos y explicación extendida

### 1. ¿Qué hace `any`?
```ts
let caos: any = 'hola';
caos.toFixed(); // ❌ en runtime
```
> ⚠️ **Error común**: confiar en el compilador, que ya se fue a dormir.

---

### 2. ¿Qué hace `unknown`?
```ts
let orden: unknown = 'hola';
orden.toUpperCase(); // ❌ compile error
```
> 🛡️ Debes verificar tipo antes de usar:
```ts
if (typeof orden === 'string') {
  orden.toUpperCase();
}
```

---

### 3. Asignación y compatibilidad
```ts
let a: any = 123;
let u: unknown = 456;

let x: number = a; // ✅
let y: number = u; // ❌ incompatible
```

---

## 🧠 Tabla resumen
| Característica | any | unknown |
|----------------|-----|---------|
| Seguridad de tipo | ❌ | ✅ |
| Requiere verificación | ❌ | ✅ |
| Permite todo | ✅ | ❌ |
| Asignable a cualquier tipo | ✅ | ❌ |
| Asignable desde cualquier tipo | ✅ | ✅ |

---

## 🧙‍♀️ Moraleja
> *`any` es como una espada sin filo: corta lo que quieras… pero también tus dedos.*