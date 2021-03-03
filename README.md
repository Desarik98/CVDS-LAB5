# *LABORATORIO 5 - MVC PRIMEFACES INTRODUCTION - 2021-1*

## **Maria Camila Fetecua – Daniel Alejandro Mejia**


## PARTE I. - JUGANDO A SER UN CLIENTE HTTP

**1.Antes de que el servidor cierre la conexión por falta de comunicación:
	•Revise la página 36 del RFC del protocolo HTTP, sobre cómo realizar una petición GET. Con esto, solicite al servidor el recurso ‘sssss/abc.html’, usando la versión 1.0 	  de HTTP.
	•Asegúrese de presionar ENTER dos veces después de ingresar el comando.
	•Revise el resultado obtenido. ¿Qué codigo de error sale?, revise el significado de este en la lista de códigos de estado HTTP.**
	301 Movido Permanentemente:Esta y todas las solicitudes futuras deben dirigirse al URI proporcionado
	
![Imagen](C:\Users\Camis\Pictures\LAB05\Imagen1.jpg)

**•¿Qué otros códigos de error existen?, ¿En qué caso se manejarán?**
	1xx informational response:Indica  que la solicitud fue recibida y comprendida. Se emite de forma provisional mientras continúa el procesamiento de la solicitud. Alerta 	     al cliente para que espere una respuesta final. 
	2xx success: Esta clase de códigos de estado indica que la acción solicitada por el cliente fue recibida, comprendida y aceptada
	4xx client errors: La solicitud contiene sintaxis incorrecta o no puede procesarse.
	5xx server errors: El servidor no completor una solicitud aparentemente válida.

**2.Ahora, solicite (GET) el recurso /html. ¿Qué se obtiene como resultado?**

IMAGEN

**3.Seleccione el contenido HTML de la respuesta y copielo al cortapapeles CTRL-SHIFT-C. Ejecute el comando wc (word count) para contar palabras con la opción -c para contar el número de caracteres:wc -c 
Pegue el contenido del portapapeles con CTRL-SHIFT-V y presione CTRL-D (fin de archivo de Linux). Si no termina el comando wc presione CTRL-D de nuevo. No presione mas de dos veces CTRL-D indica que se termino la entrada y puede cerrarle la terminal. 
Debe salir el resultado de la cantidad de caracteres que tiene el contenido HTML que respondió el servidor.**
**Claro está, las peticiones GET son insuficientes en muchos casos. Investigue: **

**¿Cuál es la diferencia entre los verbos GET y POST?**
La diferencia es que GET lleva los datos de forma "visible" al cliente (navegador web). Y su medio de envío es la URL. En cambio, en POST lleva los datos de forma "ocultos" y son enviados por un formulario cuyo método de envío es post. 

**¿Qué otros tipos de peticiones existen?**

•Método HEAD: Este método realiza una acción similar al método GET solo que a diferencia de este HEAD solo solicita los metadatos de un recurso o archivo y no todo elemento como tal.
•Método OPTIONS:Sirve para averiguar qué métodos HTTP soporta el servidor web con respecto a un recurso en concreto o en caso de que haya un * en la URI se devuelven todos los métodos soportados por el servidor.
•Método PUT:Crea/Carga un nuevo recurso al servidor, o en caso de que el objeto ya exista en el servidor reemplaza el recurso existente con el recurso que se carga.
•Método DELETE: Este método le solicita al servidor web que se borre un recurso en específico.

**4.En la práctica no se utiliza telnet para hacer peticiones a sitios web sino el comando curl con ayuda de la linea de comandos:**
curl www.httpbin.org

IMAGEN 

**Utilice ahora el parámetro -v y con el parámetro -i:**
curl -v www.httpbin.orgcurl -i www.httpbin.org

IMANGEN
IMAGEN

**¿Cuáles son las diferencias con los diferentes parámetros?**
El parametro -i significa include, esto quiere decir que solo incluirá la información de cabecera que guarda la página web. En cambio, -v significa verbose, esto quiere decir que nos dará toda la información que guarda la página más peticiones que se estén haciendo.


## PARTE II. - HACIENDO UNA APLICACIÓN WEB DINÁMICA A BAJO NIVEL.

**1.Para esto, cree un proyecto maven nuevo usando el arquetipo de aplicación Web estándar maven-archetype-webapp y realice lo siguiente**

IMAGEN

**Revise qué valor tiene el parámetro ‘urlPatterns’ de la anotación @WebServlet, pues este indica qué URLs atiende las peticiones el servlet.**
Contene Pats que son identificados por la URL 

**3. Revise en el pom.xml para qué puerto TCP/IP está configurado el servidor embebido de Tomcat (ver sección de plugins).**
Puerto 8080

**5. Abra un navegador, y en la barra de direcciones ponga la URL con la cual se le enviarán peticiones al ‘SampleServlet’. Tenga en cuenta que la URL tendrá como host ‘localhost’, como puerto, el configurado en el pom.xml y el path debe ser el del Servlet. Debería obtener un mensaje de saludo.**

IMANGEN
IMAGEN

**6.Observe que el Servlet ‘SampleServlet’ acepta peticiones GET, y opcionalmente, lee el parámetro ‘name’. Ingrese la misma URL, pero ahora agregando un parámetro GET (si no sabe como hacerlo, revise la documentación en http://www.w3schools.com/tags/ref_httpmethods.asp).**

IMANGEN

**8.En el navegador revise la dirección https://jsonplaceholder.typicode.com/todos/1. Intente cambiando diferentes números al final del path de la url.**

IMAGEN

**15.Intente hacer diferentes consultas desde un navegador Web para probar las diferentes funcionalidades.**
IMAGEN


## PARTE III

**18.En la página anterior, cree un formulario que tenga un campo para ingresar un número (si no ha manejado html antes, revise http://www.w3schools.com/html/ ) y un botón. El formulario debe usar como método ‘POST’, y como acción, la ruta relativa del último servlet creado (es decir la URL pero excluyendo ‘http://localhost:8080/’).**

IMAGEN

**20. Recompile y ejecute la aplicación. Abra en su navegador en la página del formulario, y rectifique que la página hecha anteriormente sea mostrada. Ingrese los datos y verifique los resultados. Cambie el formulario para que ahora en lugar de POST, use el método GET. ¿Qué diferencia observa?**

IMAGEN

Se observa que en el método POST simplemente sale el path sin ningún tipo de variable asignada, en cambio con el método GET aparece la variable asignada


**21. ¿Qué se está viendo? Revise cómo están implementados los métodos de la clase Service.java para entender el funcionamiento interno.**
Al principio se crea un formulario en la dirección localhost:8080/ y con el action que se ejecuta al accionar el botón, nos lleva al path /todos y al asignarle el valor id al input este valor lo coge como id y acciona el servlet que se esta ejecutando en /todos


## PARTE IV. - FRAMEWORKS WEB MVC – JAVA SERVER FACES / PRIME FACES##

Escriba una aplicación web que utilice PrimeFaces para calcular la media, la moda, la desviación estándar y varianza de un conjunto de N números reales. Este conjunto de N números reales deben ser ingresados por el usuario de manera que puedan ser utilizados para los cálculos.

**1.Al proyecto Maven, debe agregarle las dependencias mas recientes de javax.javaee-api, com.sun.faces.jsf-api, com.sun.faces.jsf-impl, javax.servlet.jstl y Primefaces (en el archivo pom.xml).**

IMAGEN

**5.Cree una página XHTML, de nombre calculadora.xhtml (debe quedar en la ruta src/main/webapp). Revise en la página 13 del manual de PrimeFaces, qué espacios de nombres XML requiere una página de PrimeFaces y cuál es la estructura básica de la misma.**
IMAGEN

**10. Si todo funcionó correctamente, realice las siguientes pruebas:**
a.Abra la aplicación en un explorador. Realice algunas pruebas de aceptación con la aplicación.
IMAGEN

b.Abra la aplicación en dos computadores diferentes. Si no dispone de uno, hágalo en dos navegadores diferentes (por ejemplo Chrome y Firefox; incluso se puede en un único 	navegador usando una ventana normal y una ventana de incógnito / privada). Haga cinco intentos en uno, y luego un intento en el otro. ¿Qué valor tiene cada uno?

IMAGEN
No son iguales, la varianza y la desviación cambian un poco en los últimos decimales

c.Aborte el proceso de Tomcat-runner haciendo Ctrl+C en la consola, y modifique el 	código del backing-bean de manera que use la anotación @SessionScoped en lugar de 	@ApplicationScoped. Reinicie la aplicación y repita el ejercicio anterior.

IMAGEN

**•Dado la anterior, ¿Cuál es la diferencia entre los backing-beans de sesión y los de 	aplicación?**
	Al ejecutar el de aplicación solo una instancia del bin va a existir en cambio de la de 	sesión se ejecuta una instancia por cada página. 

	
d.Por medio de las herramientas de desarrollador del explorador (Usando la tecla "F12" 	en la mayoría de exploradores):
	•Ubique el código HTML generado por el servidor.
IMAGEN
	•Busque el elemento oculto, que contiene el número generado aleatoriamente.
IMAGEN
	•En la sección de estilos, deshabilite el estilo que oculta el elemento para que sea visible.
IMAGEN
	•Observe el cambio en la página, cada vez que se realiza un cambio en el estilo.
IMAGEN
	•Revise qué otros estilos se pueden agregar a los diferentes elementos y qué efecto tienen en la visualización de la página.
IMAGEN
	•Actualice la página. Los cambios de estilos realizados desaparecen, pues se realizaron únicamente en la visualización, la respuesta del servidor sigue siendo la misma, ya que el 	contenido de los archivos allí almacenados no se ha modificado.

IMAGEN
	•Revise qué otros cambios se pueden realizar y qué otra información se puede obtener 	de las herramientas de desarrollador.

IMAGEN
Para facilitar los intentos del usuario, se agregará una lista de los últimos valores ingresados:
	a.Agregue en el Backing-Bean, una propiedad que contenga una lista de valores ingresados por el usuario.
	b.Cuando se reinicie la aplicación, limpie el contenido de la lista.
	c.Busque cómo agregar una tabla a la página, cuyo contenido sea la lista de listas de números.
IMAGEN
