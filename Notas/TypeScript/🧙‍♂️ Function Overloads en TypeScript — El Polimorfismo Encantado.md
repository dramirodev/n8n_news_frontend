

Las **sobrecargas de funciones** en TypeScript permiten definir múltiples firmas para una misma función, ofreciendo diferentes contratos de uso y mejorando la inferencia del compilador.

Pero con gran poder, viene gran responsabilidad: mal usadas, pueden generar más caos que claridad.

---

## 📚 Temas incluidos y explicación extendida

### 1. Definición de múltiples firmas
```ts
function parse(input: string): string;
function parse(input: number): number;
function parse(input: string | number): any {
  return typeof input === 'string' ? input.toUpperCase() : input * 2;
}
```
> ⚠️ **Error común**: no hacer coincidir implementación con firmas.

---

### 2. Firma compatible y orden
La implementación debe ser compatible con todas las firmas.
```ts
function sum(x: number): number;
function sum(x: string): string;
function sum(x: any): any {
  return typeof x === 'string' ? x + x : x + 1;
}
```
> ⚠️ **Error común**: firma general primero rompe el sistema de inferencia.

---

### 3. Con tipos genéricos
```ts
function wrap<T>(valor: T): T[];
function wrap(valor: any): any[] {
  return [valor];
}
```
> ⚠️ **Error común**: perder el tipo específico en retorno.

---

## 🧠 Tabla resumen
| Concepto | Sintaxis | Error común |
|---|---|---|
| Múltiples firmas | varias antes de impl. | Firmas no coinciden |
| Firma general | debe ir última | Rompe coincidencia |
| Genéricos | `<T>` en firma y uso | Pierde tipo al devolver |

---

## 🧙‍♀️ Moraleja
> *Una sobrecarga mal hecha es como un hechizo con dos efectos contradictorios: compila, pero nadie sabe qué diablos hará.*