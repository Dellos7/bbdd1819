
# Manipulación de documentos

Los documentos son los objetos individuales que representan algo en nuestra base de datos. Recordemos nuestra base de datos:

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

Un documento sería, por ejemplo, el siguiente:

```json
721eb7821tne21: {
    nom_video: 'League of Legends Week 15 Highlights',
    fecha_subida: '2019-02-08',
    cod_usuario: '93dh3undy38'
}
```

Es decir, un objeto que representa a un único vídeo. Podemos decir, por lo tanto, que **las colecciones se componen de documentos**. 

El nº `721eb7821tne21` es el ID del documento. Haciendo una analogía con las bases de datos relacionales, sería lo mismo que un identificador que actúa como la clave primaria de la tabla. Estos IDs, como habrás supuesto, deben ser únicos y no pueden repetirse.

El resto son simplemente los atributos del vídeo. Sería lo mismo que las columnas de una tabla en las bases de datos relacionales.

## Obtener un documento de una colección

Vamos a aprender cómo obtener un documento individual de una colección. Es parecido a obtener una lista, pero más sencillo (siempre y cuando conozcamos su ID). El método sería el siguiente:

```typescript
import { Component } from '@angular/core';
import { AngularFirestore, AngularFirestoreCollection } from '@angular/fire/firestore';
import { map } from 'rxjs/operators';
import { Observable } from 'rxjs';

@Component({
  selector: 'page-video',
  templateUrl: 'video.html'
})
export class VideoPage {

  videoDoc: AngularFirestoreDocument<any>;
  videoObs: Observable<any>;
  video: any;

  constructor(public navCtrl: NavController, public db: AngularFirestore) {
      this.obtenerVideo('721eb7821tne21');
  }

  obtenerVideo( id: string ) {
    this.videoDoc = this.db.doc(`videos/${id}`);
    this.videoObs = this.videoDoc.valueChanges();
    this.videoObs.subscribe( (res) => {
        this.video = res;
    });
}
```

Es parecido al método de listar vídeos, pero algo más sencillo. Como siempre, tenemos 3 objetos distintos:

* La **referencia** a la base de datos, en este caso al documento del vídeo.
* El **observable**, que utilizamos para que nos avise cuando hay un cambio en la base de datos y podamos enterarnos.
* El **vídeo** en sí, que es un objeto que almacena la información del vídeo propiamente dicha.

## Actualizar un documento

Actualizar y borrar documentos son probablemente las operaciones más sencillas que tenemos. 

Tenemos dos opciones de actualizar un documento:

1. De forma **no destructiva**. Es decir, actualizamos sólo los valores que queramos (los que pasemos por parámetro al método `update`).

```typescript
actualizarVideoNoDest() {
    this.videoDoc.update(this.video);
}
```

2. De forma **destructiva**. Es decir, actualizamos todo el objeto entero. En este caso, se utiliza el método `set`.

```typescript
actualizarVideoDest() {
    this.videoDoc.set(this.video);
}
```

## Borrar un documento

Borrar un documento es tan sencillo como llamar al método `delete` del documento.

```typescript
eliminarVideo() {
    this.videoDoc.delete();
}
```

---

Ves a la sección [filtrar colecciones](./filtrar-colecciones.md) para aprender como aplicar filtros a las colecciones para obtener únicamente los documentos que nos interesan.