# Promesas
 Dejadme empezar este capítulo con una afirmación un tanto contradictoria: 

> las promesas son una de las funcionalidades más vanagloriadas de ES6 y a la vez de la más infravaloradas y malentendidas.

Que quiere decir esto? Qué son valoradas por la mayoría de desarrolladores pero por los motivos equivocados y olvidando los auténticos puntos clave de las mismas. 
A menudo (creedme, he leído decenas de tutoriales al respecto ) se presentan como una alternativa a los callbacks que mejora la legibilidad. También leeréis en más de un sitio que el mayor mérito de las promesas ha sido recuperar las palabras reservadas return y sobre todo throw (pista: nunca se fueron). Ambas afirmaciones son correctas, y ambas son superficiales y nos alejan del auténtico punto clave:

> La verdadera ventaja de las promesas, lo que las hace realmente especiales, disruptivas y fantásticas es que han convertido algo implícito, una sombra, en un ciudadano de primera clase: la asincronía

"Pero si javascript es asíncrono" diréis, "tenemos los callbacks, son asíncronos" diréis, y errareis. Sí, el código javascript **es ejecutado** de forma asíncrona, pero esa es una funcionalidad del engine de javascript, no del lenguaje.
 Los callbacks por otra parte no son más que simples funciones,  son posibles gracias a otras dos grandes características del lenguaje: las **clausuras** y las **funciones como ciudadanos de primera clase**. ¿ Qué diferencia un callback de cualquier otra función? Nada.
No debemos hacer throw en un callback, no debemos devolver nada desde un callback, el primer parámetro está reservado para un posible error, en los callbacks, pero todo eso no es más que una colecci´ón de convenciones que se han acuñado tras sufrir mucho, no es nada que el lenguaje provea. Puedes hacer un callback que incumpla todas esas reglas y funcionará perfectamente. Los callbacks no son asíncronos, los callbacks son un apaño necesario en tiempos remotos y más oscuros. Un reducto que debe desaparecer.

Las promesas 
