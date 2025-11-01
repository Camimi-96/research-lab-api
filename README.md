# research-lab-api
**Nombre:** Camila San Martín Araos  
**Cohorte:** 22  
**Fecha de entrega:** 03/11/2025

### 🔹 **1. Diferencia entre HTTP y HTTPS**

- Explica qué significa cada sigla.
**HTTP** significa *HyperText Transfer Protocol*. Es el protocolo que usan los navegadores y servidores para pedir y entregar recursos (páginas HTML, JSON, imágenes, etc.). Es un protocolo cliente-servidor: el navegador (cliente) inicia solicitudes y el servidor responde con recursos o códigos de estado.
**HTTPS** significa *HyperText Transfer Protocol Secure*. Es el principal protocolo utilizado para enviar datos entre un navegador web y un sitio web. Aumenta la seguridad en la transferencia de datos. La "S" al final indica que las comunicaciones entre el navegador y el sitio web están enctriptadas. En otras palabras, es lo mismo que HTTP pero sobre una capa de seguridad (TLS - Transport Layer Security), la cual cifra la comunicación entre cliente y servidor
- Investiga cómo funciona el **cifrado SSL/TLS** en HTTPS.
El cifrado SSL (Secure Sockets Layer) es una tecnología estandarizada que permite cifrar el tráfico de datos entre un navegador web y un sitio web, protegiendo así la conexión.
El cifrado TLS (Transport Layer Security) es lo mismo que SSL pero es una versión más actualizada, moderna y segura. En otras palabras, cifra la comunicación entre el cliente y el servidor: durante la conexión se realiza un "handshake" para acordar versión de TLS, algoritmos de cifrado y para verificar la identidad del servidor mediante certificados digitales. Esto protege la confidencialidad e integridad de los datos que viajan por la red.
- ¿Por qué HTTPS es más seguro?
Porque tiene un cifrado de encriptación, tiene la autenticación y tiene la integridad de los datos. Es decir, la información no puede ser modificada durante el tránsito, ya que el navegador detecta estos cambios y bloquea la conexión.
- Muestra un ejemplo visual (puede ser una captura del candado del navegador).
[elht.jpg](https://postimg.cc/NKNHjfH2)
- ¿Qué sucede si un sitio no usa HTTPS?
La información enviada entre el usuario y el servidor no está cifrada, lo que hace vulnerable a ser interceptada y robada por hackers.

---

### 🔹 **2. Puertos de comunicación**

- Explica qué es un **puerto** en redes y por qué es importante para HTTP.
Un puerto es un número que, junto a la dirección IP, identifica un servicio en un servidor (como una "puerta" por la que entra el tráfico). Permite que un mismo servidor pueda ofrecer distintos servicios simultáneamente (por ejemplo servicios web, FTP, SSH, entre otros).
Es importante porque usa puertos específicos para establecer la comunicación entre el navegador (cliente) y el servidor web.
- Investiga el propósito de los puertos **80** y **8080**, y qué tipo de tráfico suelen manejar.
El puerto **80** es el puerto por defecto para **HTTP* y no está cifrado.
El puerto **8080** es un puerto alternativo usado frecuentemente en **desarrollo** o cuando el puerto **80** está ocupado. No añade cifrado por si mismo, es decir, sigue siendo HTTP si no cuenta con TLS
- Menciona **otros puertos conocidos** (por ejemplo: 21, 22, 443, 3306) y su función.
- Ejemplo: ¿Qué puerto utiliza HTTPS por defecto?
HTTPS utiliza el puerto **443** por defecto, el cual cuenta con cifrado TLS.
El puerto **21** es utilizado para transferencia de archivos (FTP)
El puerto **22** permite un acceso seguro por terminal (SSH)
El puerto **3306** lo utilizan desarrolladores y administradores de sistema para manejo de bases de datos (MySQL)

---

### 🔹 **3. Códigos de estado de respuesta HTTP**

- Investiga qué son los **status codes** y para qué sirven.
Son números que el servidor envía al navegador (cliente) para indicar cómo resultó una solicitud que éste le hizo. Sirven para facilitar la detección de errores como por ejemplo "página no encontrada" o "problemas del servidor", también ayudan a los desarrolladores y navegadores a entender qué hacer a continuación. Se agrupan en 5 clases: Informativos, Éxito, Redirección, Error del cliente, Error del servidor.

- Crea una **tabla organizada por categoría**:

| Categoría | Rango | Descripción general | Ejemplo de código |
| --- | --- | --- | --- |
| **1xx – Informativos** | 100–199 | El servidor recibió la solicitud y continúa el proceso. | 100 Continue |
| **2xx – Éxito** | 200–299 | La solicitud fue procesada correctamente. | 200 OK |
| **3xx – Redirección** | 300–399 | La solicitud fue redirigida a otro recurso. | 301 Moved Permanently |
| **4xx – Error del Cliente** | 400–499 | Error causado por la solicitud del cliente. | 404 Not Found |
| **5xx – Error del Servidor** | 500–599 | El servidor tuvo un problema al procesar la solicitud. | 500 Internal Server Error |

- Luego, profundiza **por qué debemos conocer y reconocer especialmente estos tres códigos:**
    - `200 OK` → cuando todo sale bien.
    - `404 Not Found` → cuando el recurso no existe o fue movido.
    - `500 Internal Server Error` → cuando el problema está en el servidor.
    > 💬 Explica con tus palabras cómo podrías usar estos códigos para diagnosticar errores en una API o en un proyecto web.
Es importante conocerlos porque son 3 de los códigos más frecuentes. En el caso del codigo 200, es importante reconocerlo porque es indicativo de que todo está funcionando como se esperaba. El código 404 nos permite identificar de forma fácil el error al decirnos que el recurso no fue encontrado, lo que facilita la corrección del código siendo programadores. Y el código 500 nos dice que el problema está en el servidor, por lo que reconocerlo nos facilita saber dónde buscar el error: logs del servidor, excepciones, configuraciones de las bases de datos o problemas en dependencias.
Para diagnosticar errores en una API, el conocimiento de estos códigos nos permite que al ejecutar la API se observen los códigos de respuesta, y así identificar el error con mayor facilidad para luego hacer las correcciones correspondientes y volver a probar.

---

### 🔹 **4. Métodos HTTP**

Investiga los principales métodos HTTP utilizados en APIs RESTful:

- **GET**, **POST**, **PUT**, **DELETE**
    
    y responde:
    
- ¿Qué hace cada uno?
- ¿En qué tipo de operación se usa (consultar, crear, actualizar, eliminar)?
- Agrega un ejemplo práctico de cada uno con una URL o pseudocódigo.
💡 *Bonus:* menciona otros métodos menos comunes como `PATCH`, `HEAD`, `OPTIONS`.

| Método | ¿Qué hace? | tipo de operación | Ejemplo (URL / pseudocódigo) |
| --- | --- | --- | --- |
| **GET** | Solicita información de un recurso del servidor sin modificarlo | Consultar, leer|requests.get("https://api.ejemplo.com/usuarios/123") |
| **POST** | Envía datos al servidor para crear un nuevo recurso | Crear| requests.post("https://api.ejemplo.com/usuarios", json={"nombre": "Naomi", "email": "naomi@mail.com"}) |
| **PUT** | Reemplaza por completo un recurso existente. También lo crea si es que no existe | Reemplazar | requests.put("https://api.ejemplo.com/usuarios/123", json={"nombre": "Naomi Núñez", "email": "naomi@mail.com"}) |
| **DELETE** | Elimina el recurso indicado del servidor. | Eliminar | requests.delete("https://api.ejemplo.com/usuarios/123") |
| **PATCH** | Actualiza parcialmente un recurso | Actualizar | import requests url = "https://api.ejemplo.com/usuarios/123" datos = {"email": "nuevoemail@mail.com"} respuesta = requests.patch(url, json=datos) |
| **HEAD** | Solicita *sólo* los encabezados del recurso a diferencia de GET que trae todo el contenido | Solicitar | import requests url = "https://api.ejemplo.com/usuarios/123" respuesta = requests.head(url) |
| **OPTIONS** | Solicita las opciones de comunicación permitidas para un recurso o servidor específico. Útil para CORS y validaciones | Consultar |import requests url = "https://api.ejemplo.com/usuarios/123" respuesta = requests.options(url)|





---

### 🔹 **5. Tema adicional sugerido: Cabeceras (Headers)**

> (Tema propuesto para investigación adicional)
> 
- ¿Qué son los **headers** en una solicitud HTTP?
Los headers son pares clave:valor que acompañan una petición o respuesta HTTP. Contienen metadatos sobre la solicitud, por ejemplo: tipo de contenido, autenticación, cacheo. 
También se le conoce como una "etiqueta" de un paquete, ya que puede contener información relevante sobre el paquete.
- ¿Qué tipo de información contienen (por ejemplo: `Content-Type`, `Authorization`, `User-Agent`)?
Content-Type: indica el tipo de contenido del cuerpo, ya sea que se envíe o se reciba.
Authorization: lleva credenciales o tokens de acceso.
User-Agent: identifica el cliente (navegador o app) que hace la petición.
Accept: qué tipos de contenido acepta el cliente.
Cookie: envía cookies guardadas al servidor.

- ¿Por qué son importantes al consumir APIs?
Permiten negociar formato de datos (Accept, Content-Type).
Controlan seguridad y autenticación (Authorization).
Permiten manejo de sesiones, estado, cache y control de versiones.
Control de contenido(tipo de datos en la petición: content-type).
Información del cliente/servidor.
Facilita la interoperabilidad (API consumible por cualquier cliente; python; java; etc).
Permite pruebas, validaciones y control.


- Muestra un ejemplo de una solicitud completa con cabeceras incluidas.

POST /api/pedidos HTTP/1.1
Host: tiendaonline.com
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64)
Content-Type: application/json
Accept: application/json
Authorization: Bearer 123abc456
Accept-Language: es-CL
Connection: keep-alive
{
  "producto": "Café molido",
  "cantidad": 2,
  "direccion_envio": "Av. Central 1234, Santiago"
}


## Reflexión
 Al investigar HTTP y HTTPS comprendí que, aunque los conceptos básicos parecen sencillos (pedir y recibir recursos), la seguridad (TLS), los códigos de estado y las cabeceras son las piezas que realmente permiten construir APIs robustas y mantenibles. Para mí, entender cómo interpretar un 404 o un 500 fue especialmente valioso: me da una guía clara para diagnosticar problemas al probar mis puntos de conexión. En adelante me esforzaré por aplicar estas herramientas (curl, inspección de headers y logs) cada vez que construya o consuma una API.
---
## Extra (Opcional)
Si quieres ir más allá, investiga también cómo funcionan las peticiones HTTP con herramientas reales, como curl, Postman o el módulo requests en Python.

Curl: es una herramienta que permite hacer peticiones HTTP desde la terminal. ej: curl -X GET https://api.ejemplo.com/usuarios/1
Postman: es una aplicación interactiva que te deja crear y probar peticiones HTTP de manera visual. ej:
[Postman-login-1.webp](https://postimg.cc/py2kry9c)
Módulo requests en Python: te permite hacer peticiones HTTP fácilmente desde tus programas.
