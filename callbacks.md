# Callbacks

## Antes de empezar

Abre una nueva pestaña en blanco en el navegador. Abre la consola del navegador (típicamente `F12`). Es en esta consola donde podremos imprimir utilizando JavaScript para hacer pruebas, al estilo de la consola típica de Java.

> **NOTA 1**: Puedes pegar el código que se muestra a continuación directamente en la consola y funcionará.

> **NOTA 2**: Tendrás que recargar la página cada vez que copies/pegues el código, ya que hay variables cuyo nombre se repite y no se pueden declarar varias veces.

## Probando los callbacks

En JavaScript, como en otros lenguajes de programación, las funciones son un tipo de dato primitivo. Esto quiere decir que podemos asignar funciones a variables, igual que lo haríamos con otro tipo de dato. Por ejemplo:

```typescript
let unNumero = 2;
let unaCadena = 'Hola';

let unaFuncion = function( num, str ) {
    console.log('el num. es: ' + num);
    console.log('la cadena es: ' + str);
};

unaFuncion( unNumero, unaCadena );
```

Imprimiría en consola:

```
el num. es: 2
la cadena es: Hola
```

Una forma más *moderna* de escribir las funciones en JavaScript sería así:

```typescript
let unNumero = 2;
let unaCadena = 'Hola';

let unaFuncion = ( num, str ) => {
    console.log('el num. es: ' + num);
    console.log('la cadena es: ' + str);
};

unaFuncion( unNumero, unaCadena );
```

Son las llamadas **funciones flecha**. Es exactamente lo mismo que lo anterior.

¿Cómo sería una función que no recibe parámetros? Así:

```typescript
let funcionSinParametros = () => {
    console.log('función sin parámetros');
};

funcionSinParametros();
```

Como hemos dicho antes, **las funciones son tipos de datos primitivos**. Y, por tanto, ¡las podemos pasar por parámetro a otras funciones! Por ejemplo:

```typescript
let funcion1 = ( otraFuncion ) => {
    let str = 'Adiós!';
    otraFuncion(str);
};

let funcion2 = ( str ) => {
    console.log(str);
};

funcion1( funcion2 );
```

Imprimiría por consola:

```
Adiós!
```

¿Qué es lo que estamos haciendo? La función `funcion1` recibe un parámetro, llamado `otraFuncion`. Como lo que está recibiendo es una función (recordemos, podemos pasar funciones por parámetro a otras funciones al ser estas un tipo de datos primitivo), podemos llamar a `otraFuncion` así: `otraFuncion(str)`, pasándole un parámetro, que en este caso es un string. 

En nuestro caso, el parámetro `otraFuncion` de la `funcion1` recibirá `funcion2`, que es otra función que hemos definido nosotros mismos. Esta función lo único que hace es imprimir lo que recibe en la consola.

Una forma más común de hacer esto es así:

```typescript
let funcion1 = ( otraFuncion ) => {
    let str = 'Adiós!';
    otraFuncion(str);
};

funcion1( (str) => {
    console.log(str);
});
```
Imprimiría exactamente lo mismo:

```
Adiós!
```

Es decir, en lugar de definir la función y guardarla en una variable (antes `funcion2`), lo que hacemos es definirla *on the fly* (al vuelo). Osea, creamos la función directamente al pasarla por parámetro, sin asignarla a ninguna variable.

El hecho de que una función reciba otra función por parámetro y llame a esa función en su definición (es exactamente lo que hacemos en `funcion1`) es lo que se conocen como ***callbacks***.

¿Por qué este nombre? *Callback* se traduce como *volver a llamar*, y se utiliza normalmente cuando queremos devolver un resultado en una función sin utilizar el `return`.

¿Pero, **por qué querríamos NO utilizar el `return`**? No es que no queramos utilizarlo, si no que a veces no podemos. En JavaScript muchas llamadas al servidor para obtener datos (por ejemplo, de una base de datos), son **asíncronas**. Podríamos decir que se ejecutan *en segundo plano*, y por tanto nos tienen que avisar ellas mismas cuando han recibido el resultado (mientras que el programa principal sigue ejecutándose).

Lo verás mucho mejor en un ejemplo. :

```typescript
let funcionAsincrona = () => {
    console.log('a');
    setTimeout( () => {
        console.log('b');
    }, 1000 );
    console.log('c');
};

funcionAsincrona();
```

El resultado es:

```
a
c
b
```

¿Por qué se imprime antes **c** que **b**? Porque `setTimeout` ejecuta la función que le pasamos (fíjate, el *callback*) después de `1000ms` (1s). Pero el resto del programa se sigue ejecutando, por tanto se ejecuta primero el `console.log('c');`, y `1000ms` después, el `console.log('b')`.

Aquí debemos fijarnos en una cosa: **no podríamos hacer un `return` dentro del `setTimeout`** para devolver un valor en `funcionAsincrona`. ¿Por qué? Porque la función finalizaría su ejecución mucho antes de que se ejecutara ese `return`, el cual se ejecutaría `1000ms` más tarde.

Entonces... ¿cómo podemos *simular* un `return` en este caso? ¡Utilizando un `callback`!

```typescript
let funcionAsincrona = ( callback ) => {
    console.log('a');
    setTimeout( () => {
        console.log('b');
        callback(3);
    }, 1000 );
    console.log('c');
};

funcionAsincrona( (resultadoFuncion) => {
    console.log('el resultado de la función es: ' + resultadoFuncion);
    console.log( resultadoFuncion + 5 );
});
```

¿Qué se imprimiría por pantalla y en qué orden?
```
a
c
b
el resultado de la función es: 3
8
```

**Lee aténtamente el código y trata de entenderlo**.

A `funcionAsincrona` le estamos pasando ahora otra función que estamos definiendo *al vuelo* al llamarla. Esta función que definimos al vuelo se ejecutará dentro del `setTimeout` de `funcionAsincrona`, e imprimirá `el resultado de la función es: 3` (fíjate que el `3` es el que pasamos como parámetro al `callback` dentro de `funcionAsincrona`). Después, podemos operar normalmente con ese resultado, hacendo una suma si queremos (`3 + 5 = 8`).

Por simplificar y resumir:

```typescript
let funcionSinCallback = () => {
    return 3;
};

let funcionConCallback = ( callback ) => {
    callback(4);
};

let res1 = funcionSinCallback();
console.log(res1);

funcionConCallback( (res2) => {
    console.log(res2);
});
```

Imprimirá:
```
3
4
```