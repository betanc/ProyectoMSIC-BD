# ProyectoMSIC-BD
Proyecto materia seguridad en bases de datos MSIC

<b>CONTEXTO</b>: 

Empresa de E-commerce de venta de medicamentos en linea, utiliza tarjetas de crédito para los pagos, los cuales realiza a través de una plataforma externa. Los servidores están ubicados en Colombia en su propio datacenter y con administración interna. El datacenter no cumple con estándares TIER. (Incluir topología).
Si bien cuentan con responsabilidades asignadas para la toma de backups, no se cuenta con un procedimiento definido y estandarizado para ello.
El motor que soporta la base de datos es MySQL Community 8.0.16 bajo un servidor Debian. 
La plataforma web no fue creada utilizando metodologías de desarrollo seguro, no se han realizado análisis de vulnerabilidades en ninguna capa (aplicación web, servidor, base de datos).
No se realiza gestión ni monitoreo de logs en ninguna de las capas.

<h2> Control ID.AM-2: Las plataformas y aplicaciones de software dentro de la organización están inventariadas</h2>

Para implementar el control ID.AM-2,  se utilizo como marco de referencia normativa, la NIST 800 y el Cybersecurity Framewor de NIST. 
Se definió una metodología estándar para la administración de los activos de información, mediante la cual se incluyó:

Proceso de identificación de activos: Desde el área de riesgos se establecen fechas de revisión y actualización de al identificación de activos, los activos se identificarán por el propietario o responsable de la información con el acompañamiento del área de ciberseguridad mediante reuniones metodológicas tipo lluvia de ideas en las cuales se usaran herramientas de apoyo como análisis de impacto, identificación y modelado de amenazas, riesgo operativo, tablas de retención documental, entre otras a fin. Dentro del proceso se debe identificar:

<br>Nombre:</br> Nombre del activo mediante el cual se puede identificar el mismo.
<br>Descripción:</br> Descripción sobre el contenido y relvancia del activo, así como componentes que apoyen su identificación
<br>Tipo:</br> Definir el tipo de activo entre: 

 - Software (No tangible que apoya generación, procesamiento, almacenamiento o eliminación de información.
 - Hardware (Dispositivos físicos que apoyan la generación, procesamiento, almacenamiento o eliminación de información.
 - Base de Datos: Información estructurada, entidades de datos con sentido y orden lógico dentro de un sistema y una relación con la organización.
<br>Propietario del Activo:</br> Ente con responsabilidad sobre la información. proceso que lo requiere para su operación.
<br>Ubicación:</br> Ubicación física y/o lógica del activo.

 
 
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
    <td class="tg-jpc1">Generalidades: Contiene 9 tablas que permiten a la organizacion desarrollar su negocio, la venta en linea de medicamentos a los usuarios registrados. <br>Motor: MySQL Community 8.0.16.<br>Tipo: Base de Datos: Relacional.<br>Información sensible: Contiene datos personales y crediticios.<br>Licenciamiento del motor: GLP.<br>Puerto: 3306 <br>Tamaño: 51k</td>
    <td class="tg-l6li">Base de datos</td>
    <td class="tg-l6li">Proceso misional</td>
    <td class="tg-l6li">Datacenter principal<br>Servidor de base de datos</td>

  </tr>
  <tr>
    <td class="tg-jpc1">Servidor de base de datos</td>
    <td class="tg-jpc1">Servidor Debian que aloja la base de datos bsm<br>Disco duro: 500GB<br>RAM: 8GB<br>Número de núcleos: 4<br></td>
    <td class="tg-jpc1">Hardware</td>
    <td class="tg-jpc1">Proceso de Tecnología</td>
    <td class="tg-jpc1">Datacenter principal</td>
    
  </tr>
  <tr>
    <td class="tg-jpc1">Firewall</td>
    <td class="tg-jpc1">Dispositivo Next Generation encargado de la seeguridad de perimetro de los sistemas de información</td>
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

En primer lugar se presenta el diagrama entidad - relacion de la base de datos "bsm", el cual permite expresar graficamente el diseño de la base de datos y la interaccion entre sus tablas.

![diagrama](https://user-images.githubusercontent.com/50051421/57118393-b6880e00-6d28-11e9-894c-1e85dbc6b70c.png)


A continuación se presentan los diagramas que de flujo normal de datos para cada actor del sistema (usuarios clientes y usuarios de gestión de la aplicación:

<i>Flujo de datos usuarios clientes:</i>

Cantidad: Entre 0 y 100 usuarios logueados por dia (rango normal).<br/>
Hora: En cualquier momento.<br/>
Frecuencia: Entre 0 y 1000 consultas por usuario (rango normal).<br/>
Origen de la consulta: Cualquier direccion IP pública.<br/>

![flujo usuario](https://user-images.githubusercontent.com/50051421/57165004-7f167180-6dbb-11e9-9d8f-e95d9b45da80.png)

<i>Flujo de datos usuarios de gestión de la aplicación:</i>

Cantidad: Entre 1 y 3 usuarios logueados por dia (rango normal).<br/>
Hora: entre 7:00 a.m. y 7:00 p.m.<br/>
Frecuencia: Entre 0 y 200 consultas al día (rango normal).<br/>
Origen de la consulta: Direcciones IP internas de la Organización.<br/>

![flujo gestion](https://user-images.githubusercontent.com/50051421/57165003-7e7ddb00-6dbb-11e9-8da6-3a27a43371f0.png)

</i>Administradores: </i><br/>
El usuario root de la base datos está en custodia del administrador de bases de datos, contratado directamente por la organización. Durante el horario laboral este administrador se conecta desde el equipo de computo asignado, ubicado en la sede principal de la organización. Durante horarios no laborales, tiene la opción de conectarse a través de una VPN, especialmente configurada para este fin. Este ultimo método fue aprobado con el objetivo de realizar ventanas de mantenimiento y solucionar incidentes.

<i>Datos que se consultan normalmente: </i><br/>
Los usuarios (compradores) pueden consultar sus ordenes,  asi como el catalogo de productos en cualquier momento, a su vez el administrador de aplicaciones consulta frecuentemente las ordenes (compras) realizadas por los usuarios con el fin de iniciar el proceso de despacho. La actualizacion del listado de productos y su categoría se realiza de forma programada e informada al Director de TI. 

<h2> Control ID.AM-6: Establecer roles y responsabilidades de Ciberseguridad</h2><p></p><br />


![ResponsabilidadesDBs](https://user-images.githubusercontent.com/50051493/57184644-016a6880-6e84-11e9-93c9-367f243e0350.png)<p></p>



![USUARIOS DBS](https://user-images.githubusercontent.com/50051493/57185210-d89aa100-6e8c-11e9-9473-3f7da41569f3.png) <p></p>


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
