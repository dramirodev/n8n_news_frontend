Cuando combinamos `as const` con tipos indexados (`T[K]`), podemos inspeccionar y validar objetos y arrays **como estructuras literales inmutables**, con resultados increíblemente precisos.

---

## 📚 Temas incluidos y explicación extendida

### 1. Indexed types sobre objetos `as const`
```ts
const config = {
  modo: 'oscuro',
  nivel: 'alto'
} as const;

type Clave = keyof typeof config;        // 'modo' | 'nivel'
type Valor = typeof config[Clave];       // 'oscuro' | 'alto'
```
> ⚠️ **Error común**: olvidar que `typeof config` necesita `keyof` o `[K]`

---

### 2. Uso con arrays literales
```ts
const formatos = ['pdf', 'doc', 'txt'] as const;
type Uno = typeof formatos[number]; // 'pdf' | 'doc' | 'txt'
```

---

### 3. Tipar dinámicamente desde estructura
```ts
function descargar(formato: typeof formatos[number]) {
  // uso seguro
}
```

---

## 🧠 Tabla resumen
| Técnica | Resultado | Nota |
|---------|-----------|------|
| `keyof typeof obj` | claves | útil para indexar |
| `typeof obj[K]` | valores | literal si `as const` |
| `[number]` en array | unión de elementos | inferencia fuerte |

---

## 🧙‍♀️ Moraleja
> *El poder del tipo indexado sobre `as const` es como un oráculo: responde exactamente lo que preguntes.*