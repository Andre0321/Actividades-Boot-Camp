# Investigación: Fundamentos de JavaScript

Actividad 5 del Boot Camp. Investigación sobre los conceptos fundamentales de JavaScript: operadores de comparación, operadores lógicos, condicionales, arrays y ciclos.

> Este documento es la versión en Markdown del archivo `Actividad Java.docx`, para poder visualizarlo directamente en GitHub.

---

## 1. Operadores de comparación

Los operadores de comparación se utilizan en JavaScript para comparar dos valores. El resultado de una comparación siempre es un valor booleano: `true` (verdadero) o `false` (falso). Son muy utilizados en condiciones como `if`, `while` y otros ciclos.

### Tabla de operadores

| Operador | Nombre | Descripción |
|----------|--------|-------------|
| `==` | Igualdad | Compara si dos valores son iguales, permitiendo conversión de tipo. |
| `===` | Igualdad estricta | Compara valor y tipo de dato. |
| `!=` | Desigualdad | Comprueba si dos valores son diferentes, permitiendo conversión de tipo. |
| `!==` | Desigualdad estricta | Comprueba si el valor o el tipo son diferentes. |
| `>` | Mayor que | Comprueba si un valor es mayor que otro. |
| `<` | Menor que | Comprueba si un valor es menor que otro. |
| `>=` | Mayor o igual que | Comprueba si un valor es mayor o igual. |
| `<=` | Menor o igual que | Comprueba si un valor es menor o igual. |

### Sintaxis

```js
valor1 operador valor2

10 > 5  // true
```

### Ejemplo 1

```js
let edad = 20;
console.log(edad >= 18);
```

Resultado: `true`, porque 20 es mayor o igual a 18.

### Ejemplo 2

```js
let contraseña = "1234";
console.log(contraseña === "5678");
```

Resultado: `false`, porque las dos cadenas de texto son diferentes.

---

## 2. Operadores lógicos

Los operadores lógicos permiten combinar o modificar condiciones. Son especialmente útiles cuando necesitamos evaluar más de una condición.

### Operadores principales

| Operador | Nombre | Funcionamiento |
|----------|--------|----------------|
| `&&` | AND (Y) | Devuelve `true` solamente cuando todas las condiciones son verdaderas. |
| `\|\|` | OR (O) | Devuelve `true` cuando al menos una condición es verdadera. |
| `!` | NOT (NO) | Invierte el resultado de una condición. |

### Ejemplo 1

```js
let edad = 25;
let tieneDocumento = true;
console.log(edad >= 18 && tieneDocumento);
```

Resultado: `true`, porque las dos condiciones se cumplen.

### Ejemplo 2

```js
let dia = "sábado";
let esFeriado = false;
console.log(dia === "sábado" || esFeriado);
```

Resultado: `true`, porque al menos una condición se cumple.

---

## 3. Condicionales

Los condicionales permiten que un programa tome decisiones dependiendo de si una condición es verdadera o falsa.

### if

Se utiliza para ejecutar un bloque de código cuando una condición es verdadera.

```js
if (condición) {
    // código
}
```

### else

Se utiliza cuando queremos ejecutar un bloque de código si la condición del `if` es falsa.

```js
if (condición) {
    // código si es verdadero
} else {
    // código si es falso
}
```

### else if

Permite evaluar varias condiciones diferentes.

```js
if (condición1) {
    // código
} else if (condición2) {
    // código
} else {
    // código
}
```

### Ejemplo 1

```js
let edad = 20;
if (edad >= 18) {
    console.log("Eres mayor de edad");
} else {
    console.log("Eres menor de edad");
}
```

Resultado: `Eres mayor de edad`.

### Ejemplo 2

```js
let nota = 4;
if (nota >= 4.5) {
    console.log("Excelente");
} else if (nota >= 3) {
    console.log("Aprobaste");
} else {
    console.log("No aprobaste");
}
```

Resultado: `Aprobaste`.

---

## 4. Arrays

Un array es una estructura de datos que permite almacenar varios valores dentro de una sola variable. Cada elemento tiene una posición llamada índice. En JavaScript los índices comienzan desde 0.

### Creación

```js
let frutas = ["Manzana", "Pera", "Banano"];
```

También se puede crear un array vacío y agregar elementos posteriormente:

```js
let frutas = [];
```

### Acceso

```js
let frutas = ["Manzana", "Pera", "Banano"];
console.log(frutas[0]);
```

Resultado: `Manzana`. El primer elemento corresponde al índice 0.

### Métodos básicos

| Método | Función |
|--------|---------|
| `push()` | Agrega un elemento al final. |
| `pop()` | Elimina el último elemento. |
| `shift()` | Elimina el primer elemento. |
| `unshift()` | Agrega un elemento al inicio. |
| `length` | Indica cuántos elementos tiene el array. |
| `includes()` | Comprueba si un elemento existe. |

### Ejemplo 1

```js
let frutas = ["Manzana", "Pera"];
frutas.push("Banano");
console.log(frutas);
```

Resultado: `["Manzana", "Pera", "Banano"]`. `push()` agregó Banano al final.

### Ejemplo 2

```js
let nombres = ["Ana", "Carlos", "Pedro"];
nombres.pop();
console.log(nombres);
```

Resultado: `["Ana", "Carlos"]`. `pop()` eliminó el último elemento.

---

## 5. Ciclos

Los ciclos permiten repetir un bloque de código varias veces mientras se cumpla una condición. Son útiles cuando necesitamos realizar una misma acción repetidamente.

### for

El ciclo `for` se utiliza cuando normalmente sabemos cuántas veces queremos repetir una acción.

```js
for (inicio; condición; incremento) {
    // código
}
```

#### Ejemplo 1

```js
for (let i = 1; i <= 5; i++) {
    console.log(i);
}
```

Resultado: `1, 2, 3, 4, 5`.

#### Ejemplo 2

```js
let frutas = ["Manzana", "Pera", "Banano"];
for (let i = 0; i < frutas.length; i++) {
    console.log(frutas[i]);
}
```

Resultado: `Manzana, Pera, Banano`.

### while

El ciclo `while` ejecuta un bloque de código mientras una condición sea verdadera.

```js
while (condición) {
    // código
}
```

#### Ejemplo 1

```js
let numero = 1;
while (numero <= 5) {
    console.log(numero);
    numero++;
}
```

Resultado: `1, 2, 3, 4, 5`.

#### Ejemplo 2

```js
let contador = 0;
while (contador < 3) {
    console.log("Hola");
    contador++;
}
```

Resultado: `Hola, Hola, Hola`.

---

## Conclusión

JavaScript cuenta con diferentes herramientas fundamentales para construir programas interactivos. Los operadores de comparación permiten comparar valores, mientras que los operadores lógicos permiten combinar condiciones. Los condicionales ayudan al programa a tomar decisiones, los arrays permiten almacenar varios datos en una misma estructura y los ciclos permiten repetir instrucciones de manera automática. Estos conceptos son fundamentales para comenzar a desarrollar aplicaciones con JavaScript y posteriormente comprender temas más avanzados como funciones, objetos, eventos y manipulación del DOM.

---

**Autor:** Andrea Rodríguez
