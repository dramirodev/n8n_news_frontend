

Con `strictPropertyInitialization` activado, TypeScript **exige** que todas las propiedades no opcionales sean inicializadas correctamente. Es la defensa mágica contra errores silenciosos por valores `undefined` no esperados.

Esta sección aborda cómo domar esta exigencia: constructores, asignación tardía, propiedades opcionales, `!` assertion y patrones de inicialización.

---

## 📚 Temas incluidos y explicación extendida

### 1. Error clásico sin inicializar
```ts
class Foo {
  bar: string; // ❌ Property 'bar' has no initializer
}
```
> ⚠️ **Error común**: olvidar inicializar en constructor.

---

### 2. Soluciones válidas
#### Opción A: Inicializar directo
```ts
bar: string = 'valor';
```
#### Opción B: Constructor
```ts
constructor(public bar: string) {}
```
#### Opción C: `!` assertion
```ts
bar!: string; // cuidado: tú prometes que la inicializarás
```

---

### 3. Uso en clases con múltiples ramas condicionales
```ts
class Mage {
  name!: string;

  setup(init: boolean) {
    if (init) this.name = 'Gandalf';
  }
}
```
> ⚠️ **Error común**: no cubrir todos los paths condicionales.

---

## 🧠 Tabla resumen
| Método | Ventaja | Peligro |
|--------|---------|--------|
| Asignación directa | Rápida | Constante | 
| Constructor | Clara y segura | Verbosa si muchas props |
| `!` assertion | Flexible | Puedes mentir |
| Propiedades opcionales `?` | Evita error | Lógica extra luego |

---

## 🧙‍♀️ Moraleja
> *Una propiedad no inicializada es como un conjuro sin invocación: está ahí, pero no funciona.*