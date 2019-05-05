# ProyectoMSIC-BD
Proyecto materia seguridad en bases de datos MSIC

<b>CONTEXTO</b>: 

Empresa de E-commerce de venta de medicamentos en linea, utiliza tarjetas de crédito para los pagos, los cuales realiza a través de una plataforma externa. Los servidores están ubicados en Colombia en su propio datacenter y con administración interna. El datacenter no cumple con estándares internacionales (TIER).
Si bien cuentan con responsabilidades asignadas para la toma de backups, no se cuenta con un procedimiento definido y estandarizado para ello.
El motor que soporta la base de datos es MySQL Community 5.6.44 bajo un servidor Debian. 
La plataforma web no fue creada utilizando metodologías de desarrollo seguro, no se han realizado análisis de vulnerabilidades en ninguna capa (aplicación web, servidor, base de datos).No se realiza gestión ni monitoreo de logs en ninguna de las capas del sistema.

<h2> Control ID.AM-2: Las plataformas y aplicaciones de software dentro de la organización están inventariadas</h2>

Para implementar el control ID.AM-2,  se utilizo como marco de referencia normativa, la NIST 800 y el Cybersecurity Framewor de NIST. 
Se definió una metodología estándar para la administración de los activos de información, mediante la cual se incluyó:

Proceso de identificación de activos: Desde el área de riesgos se establecen fechas de revisión y actualización de al identificación de activos, los activos se identificarán por el propietario o responsable de la información con el acompañamiento del área de ciberseguridad mediante reuniones metodológicas tipo lluvia de ideas en las cuales se usaran herramientas de apoyo como análisis de impacto, identificación y modelado de amenazas, riesgo operativo, tablas de retención documental, entre otras a fin. Dentro del proceso se debe identificar:

<b>Nombre:</b> Nombre del activo mediante el cual se puede identificar el mismo.

<b>Descripción:</b> Descripción sobre el contenido y relvancia del activo, así como componentes que apoyen su identificación.

<b>Tipo:</b> Definir el tipo de activo entre: 
 - Software (No tangible que apoya generación, procesamiento, almacenamiento o eliminación de información.
 - Hardware (Dispositivos físicos que apoyan la generación, procesamiento, almacenamiento o eliminación de información.
 - Base de Datos: Información estructurada, entidades de datos con sentido y orden lógico dentro de un sistema y una relación con la organización.
 
<b>Propietario del Activo:</b> Ente con responsabilidad sobre la información. proceso que lo requiere para su operación.

<b>Ubicación:</b> Ubicación física y/o lógica del activo.

El resultado es el siguiente:

<table class="tg">
  <tr>
    <td class="tg-rqnl">NOMBRE<br>DEL ACTIVO</td>
    <td class="tg-66a5">DESCRIPCIÓN</td>
    <td class="tg-rqnl">TIPO<br>DE ACTIVO DE INFORMACIÓN</td>
    <td class="tg-rqnl">PROPIETARIO<br>DEL ACTIVO</td>
    <td class="tg-rqnl">UBICACIÓN</td>

  </tr>
  <tr>
    <td class="tg-l6li">Base de datos: bsm</td>
    <td class="tg-jpc1">Generalidades: Contiene 9 tablas que permiten a la organizacion desarrollar su negocio, la venta en linea de medicamentos a los usuarios registrados. <br>Motor: MySQL Community 5.6.44.<br>Tipo: Base de Datos: Relacional.<br>Información sensible: Contiene datos personales y crediticios.<br>Licenciamiento del motor: GLP.<br>Puerto: 3306 <br>Tamaño: 61.1KB</td>
    <td class="tg-l6li">Base de datos</td>
    <td class="tg-l6li">Proceso misional</td>
    <td class="tg-l6li">Datacenter principal<br>Servidor de base de datos</td>

  </tr>
   <tr>
    <td class="tg-jpc1">Servidor de Aplicación</td>
    <td class="tg-jpc1">Servidor Debian que aloja la interfaz de presentación y mediante el cual se realizan consultas a la base de datos y se alimenta la misma<br>Disco duro: 500GB<br>RAM: 8GB<br>Número de núcleos: 4<br></td>
    <td class="tg-jpc1">Hardware</td>
    <td class="tg-jpc1">Proceso de Tecnología</td>
    <td class="tg-jpc1">Datacenter principal</td>
    
  </tr>
  <tr>
    <td class="tg-jpc1">Servidor de base de datos</td>
    <td class="tg-jpc1">Servidor Debian que aloja la base de datos bsm<br>Disco duro: 500GB<br>RAM: 8GB<br>Número de núcleos: 4<br></td>
    <td class="tg-jpc1">Hardware</td>
    <td class="tg-jpc1">Proceso de Tecnología</td>
    <td class="tg-jpc1">Datacenter principal</td>
    
  </tr>
  <tr>
    <td class="tg-jpc1">Monitor de Base de datos</td>
    <td class="tg-jpc1">Dispositivo de monitoreo encargado de consolidar registros y generar alertas de las actividades realizadas en la base de datos por los usuarios</td>
    <td class="tg-jpc1">Hardware</td>
    <td class="tg-jpc1">Proceso de Tecnología</td>
    <td class="tg-jpc1">Datacenter principal</td>
  </tr>
</table>


<h2> ID.AM-3: La comunicación organizacional y los flujos de datos están mapeados </h2>

A continuación se presenta un diagrama de arquitectura y la interacción que se tiene con la base de datos mediante la cual se pueden identificar algunos flujos de información y comunicaciones:


![diagrama arq2](https://user-images.githubusercontent.com/48939055/57187790-e6b2e680-6eb9-11e9-9829-69e4427ff432.jpg)

De acuerdo con el diagrama de arquitectura de red, con el contexto y las necesidades de negocio planteadas, se identifican principalmente cuatro roles en la base de datos.
- <b>Clientes/usuarios:</b> Usuarios que interactuan con la aplicación desde los servicios publicados en internet. Éstos interactuan con la base de datos desde la capa de presentación y operan como usuarios finales o consumidores de los servicios de la compañia.
- <b>Usuarios internos:</b> Hace referencia a empleados de la compañía los cuales tienen interacción desde la capa de presentación (Servidor de aplicación) del servicio. Acceden principalmente desde la red interna y cumplen funciones como administrar la aplicación, manejar inventarios, brindar soporte a clientes, hacer consultas sobre las tablas de productos, entre otras. Dentro de esta categoría también se incluye personal de TI que tiene interacción o administra la aplicación y el servidor de aplicación.
- <b>Administrador de Base de datos:</b> Principal responsable sobre la administración de la base de datos y sus tablas.
El usuario administrador de la base datos está en custodia de este rol, quien es contratado directamente por la organización. Durante el horario laboral se conecta desde el equipo de computo asignado, ubicado en la sede principal de la organización. Durante horarios no laborales, tiene la opción de conectarse a través de una VPN, especialmente configurada para este fin. Este ultimo método fue aprobado con el objetivo de realizar ventanas de mantenimiento y solucionar incidentes.
- <b>Monitoreo y seguridad:</b> Dentro de rol o roles se establecen responsbilidades de monitoreo sobre las acciones, cambios y trasacciones de la base de datos, de igual forma, consulta sobre roles y permisos de la base de datos, acciones realizadas por el administrador y la adecuada administración y continuidad de los controles y políticas implementadas.

<b>RELACIÓN ENTRE ROLES Y TABLAS</b>: 

En primer lugar se presenta el diagrama entidad - relacion de la base de datos "bsm", el cual permite expresar graficamente el diseño de la base de datos y la interaccion entre sus tablas.

![diagrama](https://user-images.githubusercontent.com/50051421/57118393-b6880e00-6d28-11e9-894c-1e85dbc6b70c.png)

En el diagrama anterior, se especifican las tablas y características de los datos de los cuales se pueden analizar los flujos necesarios para la operación del servicio e-commerce y el cumplimiento de la misión de la compañía. A continuación se modela de forma general, las principales interacción de los clientes y de los usuarios internos con las tablas de la base de datos:

<b>CLIENTES</b>

![flujo usuario](https://user-images.githubusercontent.com/50051421/57196876-91f98500-6f26-11e9-8819-567f6ce9c635.png)

De acuerdo con lo anterior, se identifican las siguientes tablas y su interacción con los roles definidos de la siguiente forma:

<b>-Tabla User:</b> (usuario/cliente), tabla con el registro de los usuarios o clientes registrados en la aplicación, un cliente interacua con esta tabla mediante algunas acciones o casos de uso como registrarse en la página, editar su información personal, crear un usuario y contraseña, loguearse para acceder a la aplicación, entre otras.

<b>-Tabla Product:</b> (Producto): Tabla que contiene la totalidad del inventario vigente, un cliente al interactuar con esta tabla puede realizar acciones o casos de uso como buscar productos, ver el detalle del producto y agrearlo al carrito de compras para generar una orden de pedido.

<b>-Tabla OrderDetail:</b> (Detalle de la orden): Tabla que contiene el detalle de una orden o pedido que realiza un cliente. En esta tabla el usuario realiza acciones o cuenta con casos de uso como validar el contenido del carrito, modificar o editar el pedido a realizar y finalizar el pedido, generando la orden de compra final.

A continuación se presentan los detalles más relevantes para las conexiones de los clientes:

Cantidad de clientes conectados: Entre 0 y 100 personans logueadas por dia (rango normal).<br/>
Hora: En cualquier momento.<br/>
Frecuencia: Entre 0 y 1000 consultas por cliente (rango normal).<br/>
Origen de la consulta: Cualquier direccion IP pública.<br/>

<b>USUARIOS INTERNOS:</b>

![flujo gestion](https://user-images.githubusercontent.com/50051421/57196875-91f98500-6f26-11e9-81c6-19855290738a.png)

De acuerdo a lo anterior, se identifican las siguientes tablas y su interacción con los roles definidos de la siguiente forma:

<b>-Tabla User Aplication:</b> (usuario interno), tabla correspondiente al consolidado de usuarios de la compañía que administran los productos dentro de la aplicación y que brindan soporte a usuarios o clientes, desde ésta se puede administrar su lógin y acceder a la aplicación mediante usuario y contraseña.

<b>-Tabla Product:</b> (Producto): Tabla que contiene productos y que es administrada por los usuarios internos a nivel de manejo de inventarios, inclusión o exclusión de productos, gestión de fechas de vencimiento, precios, cantidad, entre otros.

<b>-Tabla OrderDetail:</b> (Detalle de la orden): Tabla con el consolidado de las compras de los clientes, la interacción de los usuarios internos con esta tabla comprende el realizar consultas sobre los pedidos, consultar información para el despacho de productos, consulta de información financiera, soporte a usuarios, entre otras.

A continuación se presentan los detalles más relevantes para las conexiones de los usuarios internos:

Cantidad: Entre 1 y 10 usuarios logueados por dia (rango normal).<br/>
Hora: entre 7:00 a.m. y 7:00 p.m.<br/>
Frecuencia: Entre 0 y 200 consultas al día (rango normal).<br/>
Origen de la consulta: Direcciones IP internas de la Organización.<br/>

<h2> ID.AM-5: Priorización de recursos en función de su clasificación, criticidad y valor para la empresa. </h2>

<p>La clasificación de activos de información tiene como objetivo asegurar que la información recibe los niveles de protección adecuados, ya que con base en su valor y de acuerdo a otras características particulares requiere un tipo de manejo especial.</p>
<p>El sistema de clasificación de la información que se  definio para la empresa de E-Commerce se basa en las características particulares de la información, contempla la cultura y el funcionamiento interno y busca dar cumplimiento a los requerimientos  estipulados en el item relacionado con la Gestión de Activos de los estandares 27001:2013, ISO 27002, e ISO 27005.</p>

<p>La información almacenada en las bases de datos de la Plataforma de E-Commerce, dada su condición de activo estratégico, está sometida a múltiples amenazas que pueden dañarar sus intereses estratégicos, financieros, comerciales, técnicos, de imagen, operacionales, etc. Para medir la calificación del daño, se ha definido siguiente escala de calificación del riesgo:</p>


<p><span style="font-family: calibri, sans-serif;"><strong><span style="font-size: 12pt;">Clasificaciónn de la sensibilidad de la informaciónn</span></strong></span></p>
<p>La sensibilidad de una información está; vinculada a su nivel de riesgo de acuerdo a la escala definida previamente. De esta manera, se ha determinado la siguiente clasificación de la sensibilidad:</p>

![EscalaClasificacion3](https://user-images.githubusercontent.com/50051493/57186626-61730600-6ea8-11e9-9d3e-d9a7dc3e3a4b.png)



<h2> Control ID.AM-6: Establecer roles y responsabilidades de Ciberseguridad</h2>

![ResponsabilidadesDBs](https://user-images.githubusercontent.com/50051493/57184644-016a6880-6e84-11e9-93c9-367f243e0350.png)


![TiposdeUsuariosBase1](https://user-images.githubusercontent.com/50051493/57187104-c9791a80-6eaf-11e9-96a0-dccbd442ef5a.png)



<h2>Control ID.GV-4: Procesos de Gobierno y Gesti&oacute;n para la identificaci&oacute;n de los riesgos de Ciberseguridad</h2>

<p> La gestión de Riesgos de Ciberseguridad se encuentra enmarcado dentro de las disposiciones de las Normas ISO 27001:2013, e ISO 31000:2018 y basado en las buenas prácticas a nivel internacional. </p>

![MetodologiaRiesgos2](https://user-images.githubusercontent.com/50051518/57166783-e2ef6900-6dc0-11e9-8177-8807d2499caa.jpg)

<h2><strong>1. Identificaci&oacute;n de Activos de Informaci&oacute;n</strong></h2>
<p><strong>La identificaci&oacute;n de Activos de Informaci&oacute;n se realiza teniendo en cuenta todos los actores que participan para dar servicio al e-commerce a nivel de:&nbsp;</strong></p>
<ul>
<li><strong>Infraestructura tecnol&oacute;gica</strong></li>
<li><strong>Software, aplicaciones, bases de datos</strong></li>
<li><strong>Personal de la operaci&oacute;n</strong></li>
</ul>
<p><strong>Estos Activos se evidencian en los controles anteriormente nombrados, y se clasifican seg&uacute;n su nivel de importancia (ver control I.AM-5)</strong></p>
<h2><strong>2. Identificaci&oacute;n de Amenazas y Vulnerabilidades&nbsp;</strong></h2>
<p><strong>Una Amenaza tiene el potencial de causar un incidente, afectando de manera directa o indirecta los activos de informaci&oacute;n de la Corporaci&oacute;n. Por ejemplo, destrucci&oacute;n no autorizada, revelaci&oacute;n, modificaci&oacute;n, corrupci&oacute;n, indisponibilidad o p&eacute;rdida de la informaci&oacute;n</strong>.</p>
<h2><strong>3. Valoraci&oacute;n de Probabilidad e Impacto</strong></h2>
<p><strong>A continuaci&oacute;n se identifican las valoraciones que se definieron para la Gesti&oacute;n de Riesgos de Ciberseguridad:</strong></p>

<ul style="list-style-type: circle;">
<li>
<h3><strong>Probabilidad</strong></h3>
</li>
</ul>
<p>Para cada escenario de riesgo identificado se valora la probabilidad estad&iacute;stica de ocurrencia, a trav&eacute;s de una escala cuantitativa y cualitativa por cada nivel, con el fin de facilitar el proceso de evaluaci&oacute;n del mismo. Esta valoraci&oacute;n se debe realizar sin tener en cuenta los controles implementados.</p>

![Probabilidad](https://user-images.githubusercontent.com/50051518/57166818-fd294700-6dc0-11e9-887d-f1a3ff916748.jpg)

<ul style="list-style-type: circle;">
<li>
<h3><strong>Impacto</strong></h3>
</li>
</ul>
<p>El an&aacute;lisis de valoraci&oacute;n de Impacto se realiza con tres criterios definidos: reputacional, legal y/o operacional. Identificando el m&aacute;s alto de los 3, y si poseen igual valor se dejar&aacute;n todos los criterios en el escenario del riesgo con el mismo valor.</p>

![Impacto](https://user-images.githubusercontent.com/50051518/57166841-07e3dc00-6dc1-11e9-99e1-af266b33a2e9.jpg)
