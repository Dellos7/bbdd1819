
# Colecciones

Supongamos que tenemos la siguiente base de datos en Firebase:

```json
{
    videos: {
        721eb7821tne21: {
            nom_video: 'League of Legends Week 15 Highlights',
            fecha_subida: '2019-02-08',
            cod_usuario: '93dh3undy38'
        },
        219m8dh1928dn1: {
            nom_video: 'Top caídas 2018',
            fecha_subida: '2019-01-05' 
        }
    },
    listasReproduccion: {
        73ne38ny8e3k: {
            nom_lista: 'League of Legends Highlights',
            videos: [ '721eb7821tne21' ]
        }
    },
    usuarios: {
        93dh3undy38: {
            nombre: 'David',
            apellidos: 'López Castellote'
        }
    }
}
```
Es una base de datos formada por distintas colecciones: videos, listasReproduccion y usuarios. A continuación se mostrará un ejemplo para poder trabajar con la colección de vídeos en nuestra aplicación.

## Listar vídeos

La opción más compleja es la de listar, es decir, obtener una lista de los vídeos que tenemos en la base de datos de Firebase. Aunque esta opción parezca compleja al principio, y no entiendas todo lo que hace, no te preocupes puesto que utiliza conceptos bastante avanzados de programación.

```typescript
import { Component } from '@angular/core';
import { AngularFirestore, AngularFirestoreCollection } from '@angular/fire/firestore';
import { map } from 'rxjs/operators';
import { Observable } from 'rxjs';

@Component({
  selector: 'page-home',
  templateUrl: 'home.html'
})
export class HomePage {

  videosCollection: AngularFirestoreCollection<{}>;
  videosObs: Observable<any[]>;
  listaVideos: any[];

  constructor(public navCtrl: NavController, public db: AngularFirestore) {
      this.listarVideos();
  }

  listarVideos() {
    //De esta forma estamos obteniendo una referencia a la colección 'videos' de nuestra base de datos, y nos la guardamos como un atributo de la clase
    this.videosCollection = this.db.collection('videos');
    //Esta es la única forma de convertir los datos que nos devuelve Firebase a objetos capaces de ser reconocidos por nuestra aplicación.
    //Lo único con lo que nos debemos quedar es que nos estamos guardando en this.videosObs un objeto, llamado observable, que después nos permitirá obtener la lista de vídeos de la base de datos
    this.videosObs =
        this.videosCollection
            .snapshotChanges()
            .pipe(
            map(actions => actions.map(a => {
                const data = a.payload.doc.data();
                const id = a.payload.doc.id;
                return { id, ...data };
            }))
        );

    //Con el siguiente método lo que estamos haciendo es conseguir una suscripción al observable. Aquí es donde está el poder de Firebase: cada vez que se añada, elimine o actualice un vídeo en nuestra base de datos, se actualizará nuestra lista de vídeos de forma automática, sin tener que hacer nada.
    this.videosObs.subscribe( (listaVideosFirebase) => {
        //Aquí es donde recibimos la lista de vídeos de Firebase, y nos la guardamos en el atributo this.listaVideos del controlador
        this.listaVideos = listaVideosFirebase;
    });
}
```

Si nos fijamos, `this.db.collection('videos')` devuelve un objeto de la clase `AngularFirestoreCollection<{}>`, y nos lo estamos guardando en el atributo `videosCollection` del controlador. Este objeto es, al final, una referencia a la colección 'videos' de nuestra base de datos, y podemos ejecutar distintas acciones con esta colección. Las acciones que podemos ejecutar con esta referencia a la colección son básicamente listar y añadir nuevos vídeos a la base de datos.

Sin embargo, lo bonito es que siempre que queramos listar algo de nuestra base de datos, sea lo que sea, lo vamos a hacer de la misma forma. 

Como vemos, ta tenemos en el atributo 'listaVideos' del controlador la lista de vídeos de Firebase!! Ahora sólo tenemos que mostrar estos vídeos en nuestro HTML para que los puedan ver los usuarios. Para ello utilizamos la estructura tipo bucle de Angular, `*ngFor`:

```html
 <ul>
  <li *ngFor="let video of listaVideos">
    {{video.fecha_subida}}: {{video.nom_video}}
  </li>
  </ul>
```

## Añadir vídeos

Añadir nuevos vídeos a la base de datos de Firebase es mucho más sencillo que listarlos. Sería tan simple como utilizar el método `add( data: any )` de la colección que tenemos guardada en `videosCollection`. Un ejemplo sería el siguiente:

```typescript
anyadirVideo( nombreVideo: string, fechaSubida: string ) {
    this.videosCollection.add({ nom_video: nombreVideo, fecha_subida: fechaSubida });
}
```

Fácil, ¿verdad?

Ahora podríamos tener un botón en nuestro HTML que se encargara de llamar al método `anyadirVideo` y añadir vídeos a nuestra base de datos. Algo parecido a esto:

```html
<button (click)="anyadirVideo('Fortnite Tutorial', '2019-02-09')">
    Añadir vídeo
</button>
```

---

A continuación aprenderás cómo actualizar, por ejemplo, el nombre de un vídeo e incluso eliminarlo de la base de datos. Ves a la sección de [manipulación de documentos](./documentos.md).