# Promesas
 Dejadme empezar este capítulo con una afirmación un tanto contradictoria: 

> las promesas son una de las funcionalidades más vanagloriadas de ES6 y a la vez de la más infravaloradas y malentendidas.

Que quiere decir esto? Qué son valoradas por la mayoría de desarrolladores pero por los motivos equivocados y olvidando los auténticos puntos clave de las mismas. 
A menudo (creedme, he leído decenas de tutoriales al respecto ) se presentan como una alternativa a los callbacks que mejora la legibilidad. También leeréis en más de un sitio que el mayor mérito de las promesas ha sido recuperar las palabras reservadas return y sobre todo throw (pista: nunca se fueron). Ambas afirmaciones son correctas, y ambas son superficiales y nos alejan del auténtico punto clave:

> La verdadera ventaja de las promesas, lo que las hace realmente especiales, disruptivas y fantásticas es que han convertido algo implícito, una sombra, en un ciudadano de primera clase: la asincronía

"Pero si javascript es asíncrono" diréis, "tenemos los callbacks, son asíncronos" diréis, y errareis. Sí, el código javascript **es ejecutado** de forma asíncrona, pero esa es una funcionalidad del engine de javascript, no del lenguaje.
 Los callbacks por otra parte no son más que simples funciones,  son posibles gracias a otras dos grandes características del lenguaje: las **clausuras** y las **funciones como ciudadanos de primera clase**. ¿ Qué diferencia un callback de cualquier otra función? Nada.
No debemos hacer throw en un callback, no debemos devolver nada desde un callback, el primer parámetro está reservado para un posible error, en los callbacks, pero todo eso no es más que una colección de convenciones que se han acuñado tras sufrir mucho, no es nada que el lenguaje provea. Puedes hacer un callback que incumpla todas esas reglas y funcionará perfectamente. Los callbacks no son asíncronos, los callbacks son un apaño necesario en tiempos remotos y más oscuros. Un reducto que debe desaparecer.

Las promesas son un grandísimo avance para el lenguage y para los patrones que se pueden implementar con el, pero como todo gran poder, conllevan una gran responsabilidad (como todo en javascript). 
Al contratio que con muchas otras carácterísticas, en el caso de las promesas es mejor hablar primero de lo que NO se debe hacer. Algunos de los errores más comunes que debemos evitar son:

* Promise hell. Pensabas que lo peor de los callbacks era la pirámide de la muerte ? Pues con las promesas es igual de fácil incurrir en este antipatrón.
* Romper la cadena: Esta es probablemente la regla más importante de las promesas. NUNCA, jamás debemos romper la cadena de promesas
* Crear promesas innecesariamente
* Encadenar promesas de forma incorrecta (ejecutándolas donde no toca)

## Promesas en práctica

Ya está bien de introducciones, show me the code, qué aspecto tiene una promesa ? 
Por simplicidad, vamos a empezar con una promesa ya existente, es decir, a operar con promesas, no crearlas. Imagina que tenemos una función que devuelve una promesa, podría ser algo así:

```
// Callbacks
database.find({ id: 1 }, 
  (err, result) => console.log(result));

// Promesas
database.find({ id: 1 })
.then(result => console.log(result));
```

Así de sencillo, hacemos una búsqueda en la base de datos, esa búsqueda nos devuelve una promesa y automáticamente podemos emepezar a encadenar lógica. Esta capacidad de encadenamiento es lo que hace a las promesas tan flexibles y composables.

Antes de seguir explorando esta capacidad de encadenamiento déjame introducirte un par de reglas al respecto:
* Todo lo que se devuelva en cualquier función dentro de una promesa o cadena de promesas es automáticamente encapsulado en una promesa
* Cualquier promesa devuelta dentro de otra promesa o cadena de promesas es automáticamente resuelta y su valor pasa a la siguiente sección de la cadena.

Déjame explicárme con código. La primera regla significa que los dos snippers de código a continuación son equivalentes

```js
users.find({ id: 1 })
.then(user => user.age + 1)
.then(newAge => console.log(newAge)

users.find({ id: 1 })
.then(user => Promise.resolve(user.age + 1))
.then(newAge => console.log(newAge)
```

Recordais el fallo sobre instanciar promesas de forma innecesaria ? Pues el segundo ejemplo es un buen ejemplo de ello.

La segunda regla, esa sobre promesas dentro de promesas es precisamente donde las promesas empiezan a desmarcarse de los callbacks. Imaginemos que tenemos que recuperar un usuario de la base de datos, una vez que conocemos el id de ese usuario queremos buscar sus mensajes asociados, bien, hagámos uso del encadenamiento con de promesas y comparémoslo con los callbacks ya que estamos

```
// Callbacks
users.find( { name: 'Juan', surname: 'Lopez' }, 
    (err,user) => messages.find({user_id: user.id}), 
        (err,messages) => console.log(messages));
        
// Promesas
users.find({ name: 'Juan', surname: 'Lopez' })
.then(user => messages.find({user_id: user.id})
.then(messages => console.log(messages)
```

Esa pirámide empeiza a resultarte familiar verdad? No te preocupes, estás en el sitio adecuado
