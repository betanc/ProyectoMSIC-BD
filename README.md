# ProyectoMSIC-BD
Proyecto materia seguridad en bases de datos MSIC

<b>CONTEXTO</b>: 

Empresa Colombiana E-commerce de venta de medicamentos en linea, utiliza tarjetas de crédito para pagos, los cuales realiza a través de una plataforma externa. Los servidores están ubicados en Colombia en su propio datacenter y con administración interna. Si bien cuentan con responsabilidades asignadas para la toma de backups, no se cuenta con un procedimiento definido y estandarizado para ello.
El motor que soporta la base de datos es MySQL Community 5.6.44 bajo un servidor Debian. 
La plataforma web no fue creada utilizando metodologías de desarrollo seguro, no se han realizado análisis de vulnerabilidades en ninguna capa (aplicación web, servidor, base de datos). No se realiza gestión ni monitoreo de logs en ninguna de las capas del sistema.

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


<h2> Control ID.AM-3: La comunicación organizacional y los flujos de datos están mapeados </h2>

A continuación se presenta un diagrama de arquitectura y la interacción que se tiene con la base de datos mediante la cual se pueden identificar algunos flujos de información y comunicaciones:


![diagrama arq4](https://user-images.githubusercontent.com/48939055/57202032-30590b00-6f66-11e9-8cec-658371ec5028.jpg)

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


A continuación se presentan imágenes de la base de datos evidenciando las tablas anteriormente mencionadas:

Tabla usuarios:
![Captura usuarios](https://user-images.githubusercontent.com/50051421/57201382-f1bf5280-6f5d-11e9-9118-984ac705bc4f.JPG)

Tabla productos:
![Captura productos](https://user-images.githubusercontent.com/50051421/57201381-f1bf5280-6f5d-11e9-89d4-fe75b62bef45.JPG)

Tabla detalle de la orden:
![Captura order detail](https://user-images.githubusercontent.com/50051421/57201380-f1bf5280-6f5d-11e9-8448-a7764dde67bf.JPG)


<h2> Control ID.AM-5: Priorización de recursos en función de su clasificación, criticidad y valor para la empresa. </h2>

<p>La información almacenada en las bases de datos de la Plataforma de E-Commerce, dada su condición de activo estratégico, está sometida a múltiples amenazas que pueden dañarar sus intereses estratégicos, financieros, comerciales, técnicos, de imagen, operacionales, etc. La clasificación de activos de información tiene como objetivo asegurar que la información recibe los niveles de protección adecuados, ya que con base en su valor y de acuerdo a otras características particulares requiere un tipo de manejo especial.</p>
<p>El sistema de clasificación de la información que se  definio para la empresa de E-Commerce se basa en las características particulares de la información, contempla la cultura y el funcionamiento interno y busca dar cumplimiento a los requerimientos  estipulados en el item relacionado con la Gestión de Activos de los estandares 27001:2013, ISO 27002, e ISO 27005.</p>


<p><span style="font-family: calibri, sans-serif;"><strong><span style="font-size: 12pt;">Clasificaciónn de la sensibilidad de la informaciónn</span></strong></span></p>
<p>La sensibilidad de una información está; vinculada a su nivel de riesgo de acuerdo a la escala definida previamente. De esta manera, se ha determinado la siguiente clasificación de la sensibilidad:</p>

![Clasificacion modificada222](https://user-images.githubusercontent.com/50051493/57199910-583a7580-6f4a-11e9-9b05-62566bf6b7d0.png)


![ClasificacionInfoActivos222](https://user-images.githubusercontent.com/50051493/57199920-7902cb00-6f4a-11e9-81bf-aa8c8d895d34.PNG)

<h2> Control ID.AM-6: Establecer roles y responsabilidades de Ciberseguridad</h2>

![Organigrama Empresa 3 pptx](https://user-images.githubusercontent.com/50051493/57201897-9f356480-6f64-11e9-966e-f8acb6e311f4.png)


![TiposdeUsuariosBase1](https://user-images.githubusercontent.com/50051493/57187104-c9791a80-6eaf-11e9-96a0-dccbd442ef5a.png)

<h2>Control ID.GV-3: Requisitos legales y reglamentarios relacionados con la ciberseguridad</h2>

A continuación se presentan los requisitos legales y reglamentarios relacionados con la ciberseguridad identificados para la organización:

<table class="tableizer-table">
<thead><tr class="tableizer-firstrow"><th>Jerarquía de la Norma</th><th>Número / Fecha</th><th>Título / Descripción</th></tr></thead><tbody>
 <tr><td>Constitución Política</td><td>1991</td><td>Constitución Política. Artículo 15. Todas las personas tienen derecho a su intimidad personal y familiar y a su buen nombre, y el Estado debe respetarlos y hacerlos respetar. De igual modo, tienen derecho a conocer, actualizar y rectificar las informaciones que se hayan recogido sobre ellas en bancos de datos y en archivos de entidades públicas y privadas.</td></tr>
 <tr><td>Ley Estatutaria</td><td>1266 de 2008</td><td>Por la cual se dictan las disposiciones generales del habeas data y se regula el manejo de la información contenida en bases de datos personales, en especial la financiera, crediticia, comercial, de servicios y la proveniente de terceros países y se dictan otras disposiciones.</td></tr>
 <tr><td>Ley Estatutaria</td><td>1581 de 2012</td><td>Por la cual se dictan disposiciones generales para la protección de datos personales.</td></tr>
  <tr><td>Ley</td><td>527 de 1999</td><td>Por medio de la cual se define y reglamenta el acceso y uso de los mensajes de datos, del comercio electrónico y de las firmas digitales, y se establecen las entidades de certificación y se dictan otras disposiciones.</td></tr>
  <tr><td>Ley </td><td>633 de 2000</td><td>Articulo 91: Todas las páginas Web y sitios de Internet de origen colombiano que operan en el Internet y cuya actividad económica sea de carácter comercial, financiero o de prestación de servicios, deberán inscribirse en el Registro Mercantil y suministrar a la Dirección de Impuestos y Aduanas Nacionales DIAN, la información de transacciones económicas en los términos que esta entidad lo requiera.</td></tr>
 <tr><td>Ley</td><td>1480 de 2011</td><td>Por medio de la cual se expide el Estatuto del Consumidor y se dictan otras disposiciones.</td></tr>
 <tr><td>Ley</td><td> 1735 de 2014</td><td>Por la cual se dictan medidas tendientes a promover el acceso a los servicios financieros transaccionales y se dictan otras disposiciones.</td></tr>
 <tr><td>Decreto</td><td>2952 de 2010</td><td>Por el cual se reglamentan los artículos 12 y 13 de la Ley 1266 de 2008.</td></tr>
 <tr><td>Decreto</td><td>1377 de 2013</td><td>Por el cual se reglamenta parcialmente la Ley 1581 de 2012.</td></tr>
 <tr><td>Decreto</td><td>886 de 2014</td><td>Por el cual se reglamenta el artículo 25 de la Ley 1581 de 2012, relativo al Registro Nacional de Bases de Datos</td></tr>
 <tr><td>Decreto</td><td>1747 de 2000</td><td>Por el cual se reglamenta parcialmente la Ley 527 de 1999, en lo relacionado con las entidades de certificación, los certificados y las firmas digitales.</td></tr>
 <tr><td>Circular Externa Superfinanciera</td><td>008 de 2018 </td><td>Imparte instrucciones en materia de requerimientos mínimos de seguridad y calidad para la realización de operaciones.</td></tr>
 <tr><td>Circular Externa Superintendencia de Industria y Comercio</td><td>Circular única agosto de 2001</td><td>Título V Protección de datos personales</td></tr>
  <tr><td>EStandar PCI DSS </td><td>versión 3.2.1 </td><td>Estándar de Seguridad de Datos para la Industria de Tarjeta de Pago </td></tr>
</tbody></table>


<h2>Control ID.GV-4: Procesos de Gobierno y Gesti&oacute;n para la identificaci&oacute;n de los riesgos de Ciberseguridad</h2>

<p> La gestión de Riesgos de Ciberseguridad se encuentra enmarcado dentro de las disposiciones de las Normas ISO 27001:2013, e ISO 31000:2018 y basado en las buenas prácticas a nivel internacional. </p>

![MetodologiaRiesgos2](https://user-images.githubusercontent.com/50051518/57166783-e2ef6900-6dc0-11e9-8177-8807d2499caa.jpg)

<h2><strong>1. Identificaci&oacute;n de Activos de Informaci&oacute;n</strong></h2>
<p>La identificaci&oacute;n de Activos de Informaci&oacute;n se realiza teniendo en cuenta todos los actores que participan para dar servicio al e-commerce a nivel de:&nbsp;</p>
<ul>
<li>Infraestructura tecnol&oacute;gica</li>
<li>Software, aplicaciones, bases de datos</li>

</ul>
<p>Estos Activos se evidencian en los controles anteriormente nombrados, y se clasifican seg&uacute;n su nivel de importancia (ver control I.AM-5)</p>
<h2><strong>2. Identificaci&oacute;n de Amenazas y Vulnerabilidades&nbsp;</strong></h2>
<p>Una Amenaza tiene el potencial de causar un incidente, afectando de manera directa o indirecta los activos de informaci&oacute;n de la Corporaci&oacute;n. Por ejemplo, destrucci&oacute;n no autorizada, revelaci&oacute;n, modificaci&oacute;n, corrupci&oacute;n, indisponibilidad o p&eacute;rdida de la informaci&oacute;n.</p>
<h2><strong>3. Valoraci&oacute;n de Probabilidad e Impacto</strong></h2>
<p>A continuaci&oacute;n se identifican las valoraciones que se definieron para la Gesti&oacute;n de Riesgos de Ciberseguridad:</p>

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

<b>IDENTIFICACIÓN DE RIESGOS: </b>
<p>A continuación se relacionan los escenarios de riesgos identificados, con su respectiva valoración de probabilidad e impacto y el resultado arroja el Riesgo Inherente.</p>

![Riesgos1](https://user-images.githubusercontent.com/50051518/57200768-50cc9980-6f55-11e9-929c-05cd88675c3d.jpg)

![Imagen2](https://user-images.githubusercontent.com/50051518/57200771-5924d480-6f55-11e9-8d02-86d94a9aef06.jpg)

<b>MAPA DE CALOR:</b> 
<p><strong>En el mapa de calor se observa la ubicación de los 7 riesgos identificados según su valoración: </strong></p>

![MapaRIesgos](https://user-images.githubusercontent.com/50051518/57200772-5924d480-6f55-11e9-984b-b576e6b9f16a.jpg)


<h2>Control PR.AC-1: las identidades y credenciales se emiten, gestionan, verifican, revocan y auditan.</h2>

Para implementar este control en primera medida se crean los diferentes roles en la base de datos y se asignan los permisos correspondientes, de conformidad con lo descrito en los controles de identificación:

![creacion de roles y privilegios](https://user-images.githubusercontent.com/50051421/57586313-d0a8b580-74b9-11e9-9e5b-5789c4f636a2.png)

Los privilegios asignados a cada rol son los siguientes:

* rol_administrador: Todos los privilegios en todo las bases de datos del sistema.

* rol_propietario: INSERT, SELECT, UPDATE, DELETE en la base de datos "bsm".

* rol_conexion: SELECT en la base de datos "bsm".

* rol_operario Todos los privilegios e la base de datos "bsm". 

Una vez definidos los roles se crean 4 usuarios y se asignan a cada unos de los roles definidos de la siguiente forma:

![crear usuarios](https://user-images.githubusercontent.com/50051421/57586415-26ca2880-74bb-11e9-8416-5d768630e03e.png)

![asignacion de roles](https://user-images.githubusercontent.com/50051421/57587135-99400600-74c5-11e9-9363-b46d11fd357c.png)


<h2> Control ID.RA-4: Se identifican potenciales impactos y probabilidades sobre el negocio</h2>



<h2> Control PR.DS-3: Los activos se administran formalmente mediante un proceso de eliminación, transferencias y disposición</h2>


<h2> Control PR.DS-4: Capacidad adecuada para garantizar la disponibilidad</h2>

<h2>REFERENCIAS </h2>
<li>Gestión de Riesgos: ISO 31000:2018</li>
<li>Gestión de Activos: ISO 27001:2013</li>
<li>NIST Cybersecurity Framework 1.1</li>
<li>Marco Regulatorio:www.sic.gov.co/repositorio-de-normatividad</li>
<li>Marco Regulatorio:https://www.superfinanciera.gov.co/inicio/normativa-60706</li>
<li>Seguridad en MySQL:https://dev.mysql.com/doc/refman/8.0/en/security-html</li>
<li>Control de acceso MySql:https://dev.mysql.com/doc/refman/8.0/en/access-control.html</li>
