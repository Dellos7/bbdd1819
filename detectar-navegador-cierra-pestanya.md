# Cómo detectar cuando se cierra una ventana del navegador

El código en JavaScript lo he puesto aquí: [https://codepen.io/dellos7/pen/vwxEmL?editors=0010#0](https://codepen.io/dellos7/pen/vwxEmL?editors=0010#0), pero es este:

```javascript
//Se ejecuta cuando se cierra la pestaña del navegador
window.addEventListener('beforeunload', () => {
  //Imprime "cerrando pestaña del navegador!!! en la consola"
  console.log('cerrando pestaña del navegador!!!');
  //Abre la página "https://ionicframework.com/" en una nueva pestaña
  window.open("https://ionicframework.com/", '_blank');
});
```
He hecho un pequeño vídeo que lo demuestra:

<iframe width="560" height="315" src="https://www.youtube.com/embed/WsdQeDfRYZU" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>