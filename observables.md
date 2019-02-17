
# Observables

**Podemos pensar en un observable como si fuera una función**. De hecho, tanto el observable como la función tiene la misma finalidad: devolver valores. 

**La diferencia** entre un observable y una función es que la función devuelve uno (o varios) valores de golpe. Pero sólo una vez cada vez que se le invoca. Al observable se le invoca una vez (realmente, te *suscribes* al observable), y puede devolver múltiples valores a lo largo del tiempo.

Veamos un ejemplo. Así es como se utilizan las funciones:

```typescript
let foo = function() {
  console.log('Hola');
  return 42;
  return 100; // código muerto. Nunca se llegará a ejecutar
}

console.log('antes');
console.log(foo());
console.log('después');
```

Resultado en la consola:

```
antes
Hola
42
después
```

```typescript
let foo = Observable.create(function (observer) {
  console.log('Hola');
  observer.next(42);
  observer.next(100); // devolver otro valor
  observer.next(200); // devolver otro valor
});

console.log('antes');
foo.subscribe(function (num) {
  console.log(num);
});
console.log('después');
```

Resultado en la consola:

```
antes
Hola
42
100
200
después
```

Como podemos ver, con la función `next` del objeto recibido por parámetro en la función `create` podemos devolver múltiples valores con solo invocar una vez al observable.

La función `subscribe` del observable simula que nos estamos suscribiendo a ese observable. Todo aquel que se suscribe al observable se llama observer. De esta forma, en la función *callback* que pasamos por parámetro al método `subscribe` es donde podemos recibir los distintos valores devueltos por el observable.

Lo más interesante de los observables es, sin duda, que **permiten obtener valores de forma asíncrona**. Es decir, nos podemos suscribir al observable, recibir un valor, y al cabo de un tiempo (unos segundos, minutos, etc.) podemos volver a recibir otro valor.

Un ejemplo sería el siguiente:

```typescript
let foo = Observable.create(function (observer) {
  console.log('Hola');
  observer.next(42);
  observer.next(100); // devolver otro valor
  observer.next(200); // devolver otro valor
  setTimeout(() => {
    observer.next(300); // devuelve otro valor al cabo de 100ms (1s)
  }, 1000);
});

console.log('antes');
foo.subscribe(function (num) {
  console.log(num);
});
console.log('después');
```

El resultado sería el siguiente:

```
antes
Hola
42
100
200
después
300
```

Si nos fijamos, se imprimirá el valor `300` después del valor `después`, ya que se ejecuta de forma asíncrona utilizando la función `setTimeout`.

Si quisiéramos en algún momento que el observable dejara de devolvernos valores, podríamos hacerlo así:

`foo.unsubscribe();`