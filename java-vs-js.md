```typescript
class Campeon {
    name;
    title;
    tags;

    constructor( name, title, tags ) {
        this.name = name;
        this.title = title;
        this.tags = tags;
    }

    getName() {
        return this.name;
    }

    setName( name ) {
        this.name = name;
    }

}

let campeon = new Campeon('Ahri', 'the Nine-Tailed Fox', [ 'Mage', 'Assassin' ]);
console.log( campeon.getName() );

// Ahri
```

```java
class Campeon {
    private String name;
    private String title;
    private String tags; 

    public Campeon( String name, String title, String tags ) {
        this.name = name;
        this.title = title;
        this.tags = tags;
    }

    public String getName() {
        return this.name;
    }

    public void setName( name ) {
        this.name = name;
    }
}

public static void main( String[] args ) {
    Campeon campeon = new Campeon( 'Ahri', 'the Nine-Tailed Fox', { 'Mage', 'Assassin' } );
    System.out.println( campeon.getName() );

    //Ahri
}
```

```typescript
class Campeon {
    private name: string;
    private title: string;
    private tags: string[];

    constructor( private name: string, private title: string, tags: string[] ) {
        //Se asignarán solas
    }

    public getName(): string {
        return this.name;
    }

    public setName( name ) {
        this.name = name;
    }

}

let campeon: Campeon = new Campeon('Ahri', 'the Nine-Tailed Fox', [ 'Mage', 'Assassin' ]);
console.log( campeon.getName() );

// Ahri
```

```typescript

let a: string = "abcde";
let b: number = 123;
let c: boolean = true;
let d: string[] = [ "abc", "def", "ghi" ];
let e: number[] = [ 123, 456, 789 ];

let fecha: Date = new Date();
let fechaStr: string = fecha.toISOString();
console.log(fechaStr);
// 2019-03-04T16:15:47.330Z

const inmutable: string = "soy una variable inmutable";
inmutable = "otro valor";
//Error. Uncaught TypeError: Assignment to constant variable.

let animal: string = "gato";
if( a === "gato" ) {
    console.log("es un gato");
}
else if( a === "perro" ) {
    console.log("es un perro");
}
else {
    console.log("no es ni gato ni perro");
}
//es un gato

let animales: string[] = [ "gato", "perro", "pájaro" ];
for( let animal of animales ) {
    console.log(animal);
}
//gato
//perro
//pájaro

for( let i = 0; i < animales.length; i++ ) {
    console.log(animales[i]);
}
//gato
//perro
//pájaro

let fecha: Date = new Date();
let fechaStrISO: string = fecha.toISOString();
console.log(fechaStr);
// 2019-03-04T16:15:47.330Z
let fechaStrLocal: string = fecha.toLocaleDateString();
console.log(fechaStrLocal);
// 4/3/2019
let horaStrLocal: string = fecha.toLocaleTimeString();
console.log(horaoraStrLocal);
// 16:15:47
let fechaHoraStrLocal: string = fecha.toLocaleString();
console.log(fechaHoraStrLocal);
// 4/3/2019 16:15:47
let dia: number = fecha.getDate(); // 4
let mes: number = fecha.getMonth(); // 2 (empiezan en 0. Enero 0, febrero 1...)
let anyo: number = fecha.getFullYear(); // 2019
let hora: number = fecha.getHours(); // 16
let minutos: number = fecha.getMinutes(); // 15
let segundos: number = fecha.getSeconds(); // 47

console.log( "mensaje informativo" );
console.error( "mensaje de error" );
console.warn( "mensaje de advertencia" );

let asignatura: any = {
    'nombre': 'Bases de datos',
    'codigo': '1CFSL-BBDD',
    'curso': {
        'nombre': 'Grado Superior Desarrollo Aplicaciones Multiplataforma',
        'nivel': 1,
        'instituto': 'IES Caminàs'
    },
    'grupo': '1CFSL',
    'num_alumnos': 18,
    'alumnos': [
        {
            'nombre': 'Cristina',
            'apellidos': 'Gil Morales'
        },
        {
            'nombre': 'Oscar',
            'apellidos': 'Miralles López'
        }
    ]
    
};

console.log(asignatura.codigo);
// 1CFSL-BBDD
console.log( `La asignatura tiene ${asignatura.num_alumnos} alumnos` );
// La asignatura tiene 18 alumnos
console.log(asignatura.curso.nombre);
// Grado Superior Desarrollo Aplicaciones Multiplataforma
console.log(asignatura.alumnos[1].nombre);
// Oscar
```

```typescript
let suma = function( num1, num2 ) {
    return num1 + num2;
};

console.log( suma( 2, 3 ) );
// 5
```

```typescript
let suma = ( num1, num2 ) => {
    return num1 + num2;
};

console.log( suma( 2, 3 ) );
// 5
```

```typescript
//Recibe los números a sumar y una función por parámetro
let sumaConCallback = ( num1, num2, callback ) => {
    let res = num1 + num2;
    callback( res );
};

//Paso por parámetro los números a sumar y la función callback
sumaConCallback( 2, 3, (resultadoSuma) => {
    console.log(resultadoSuma);
});

// 5
```

```typescript
//Recibe los números a sumar y una función por parámetro
let sumaConCallback = ( num1, num2, callback ) => {
    let res = num1 + num2;
    callback( res );
};

let funcionCallback = ( resultadoSuma ) => {
    console.log(resultadoSuma);
};

//Paso por parámetro los números a sumar y la función callback
sumaConCallback( 2, 3, funcionCallback);

// 5
```

```typescript
let suma = function(num1, num2) {
    console.log(`-> El num1 recibido por parámetro es ${num1}`);
    console.log(`-> El num2 recibido por parámetro es ${num2}`);
    return num1 + num2;
};

let resultadoSuma = suma( 2, 3 );
console.log(`La suma de 2 y 3 es ${resultadoSuma}`);
```


```typescript
let listaAnimales = [ 'perro', 'gato', 'pajaro', 'hamster', 'conejo', 'cobaya' ];
let tamLista = listaAnimales.length;// Obtiene el tamaño de la lista
console.log(tamLista);// 6

let nuevoAnimal = 'tortuga';
listaAnimales.push(nuevoAnimal);// Añade un elemento a la lista

let animalPrimeraPosicion = listaAnimales[0];
console.log(animalPrimeraPosicion);// perro

listaAnimales.splice(2, 1);// Elimina 1 elemento a partir del indice 2 (en este caso, 'pajaro')

console.log(listaAnimales);// ["perro", "gato", "hamster", "conejo", "cobaya", "tortuga"]

listaAnimales[1] = 'tigre';// Modifica 'gato' por 'tigre'

console.log(listaAnimales);// ["perro", "tigre", "hamster", "conejo", "cobaya", "tortuga"]
```