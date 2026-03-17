Integrantes
Marielena Velasquez Escobar
Ariel Esau Yanes Quintanilla

* Explique con sus propias palabras qué es Vue.js y cuál es su función dentro de la
página web desarrollada.

Vue.js es un framework de JavaScript que permite crear interfaces web dinámicas e interactivas de forma sencilla. 
Su principal función es conectar los datos con lo que el usuario ve en pantalla.

Dentro de esta aplicación, Vue.js se utilizó para manejar la información ingresada por el usuario, actualizar 
automáticamente la interfaz cuando se agregan vehículos, mostrar listas dinámicas y validar los datos sin necesidad
de recargar la página.


 * Describa qué variables reactivas utilizó en su aplicación y cuál es la función de
cada una dentro del sistema.


Las variables reactivas utilizadas en el sistema son:

cliente: almacena el nombre del cliente que lleva el vehículo.
placa: guarda la placa del vehículo ingresado.
servicio: indica el tipo de servicio solicitado (aceite, frenos, diagnóstico, etc.).
prioridad: define la urgencia del servicio (alta, media o baja).
vehiculos: es un arreglo donde se almacenan todos los vehículos registrados.
mensaje: muestra mensajes al usuario, como confirmaciones de registro o eliminación.
errores: guarda los mensajes de error cuando los datos no son válidos.
busqueda: permite filtrar los vehículos por placa.

Estas variables son reactivas porque cuando cambian, Vue actualiza automáticamente la interfaz.


* Explique la diferencia entre las siguientes directivas utilizadas en su proyecto: v-
bind y v-model


La directiva v-bind se utiliza para enlazar atributos de HTML con datos de Vue. Por ejemplo, se usa para deshabilitar 
un botón dependiendo de una condición.
La directiva v-model se utiliza para enlazar los datos de un input con una variable. Esto permite que lo que el
usuario escriba se guarde automáticamente en el sistema.


* Mencione al menos un ejemplo de evento utilizado dentro de su aplicación.

@submit.prevent="agregarVehiculo"
Este evento se activa cuando el usuario envía el formulario. Su función es evitar que la página se recargue
y ejecutar la función que agrega el vehículo.

También se utilizó el evento
@click="eliminarVehiculo(index)"
para eliminar un registro de la lista.


* Explique para qué utilizó la directiva v-for dentro de su aplicación.

La directiva v-for se utilizó para recorrer el arreglo de vehículos y mostrarlos en una tabla.

Gracias a esto, cada vehículo agregado aparece automáticamente en la interfaz sin necesidad de recargar la página.

 
* Describa en qué situación utilizó v-if y qué problema resuelve dentro de su
interfaz.

La directiva v-if se utilizó en varias situaciones:
para mostrar mensajes de éxito
para mostrar errores de validación
para indicar que no hay vehículos registrados
para mostrar cuando no hay resultados en la búsqueda


* Explique cómo se realiza la validación de datos en su aplicación y por qué es
importante validar la información ingresada por el usuario.

La validación de datos se realiza dentro de la función que agrega vehículos. Antes de guardar la información, 
el sistema verifica:

que el nombre del cliente no esté vacío
que la placa no esté vacía
que la placa tenga un formato válido o longitud mínima
que el servicio haya sido seleccionado
que la prioridad haya sido seleccionada

Si hay errores, estos se muestran en pantalla y no se guarda el registro.

La validación es importante porque evita errores, datos incompletos y problemas en el sistema, 
asegurando que la información sea correcta y útil.
