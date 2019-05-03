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

• Identificar y documentar los flujos de datos que son permitidos desde y hacia las bases de datos.

En primer lugar se presenta el diagrama entidad - relacion de la base de datos "bsm", el cual permite expresar graficamente el diseño de la base de datos y la interaccion entre sus tablas.

![diagrama](https://user-images.githubusercontent.com/50051421/57118393-b6880e00-6d28-11e9-894c-1e85dbc6b70c.png)

Quienes son los administradores: El usuario root, esta en custodia del Administrador de Bases de datos, contratado directamente por la organización 

Desde donde se conectan: Durante el horario laboral, el admnistrador de la base de datos se conecta desde el equipo de computo asignado, ubicado en la sede principal de la organización. Durante horarios no laborales,  tiene la opción de conectarse a través de una VPN, especialmente configurada para este fin. Este ultimo método fue aprobado para ventanas de mantenimiento y solución de incidentes.

Datos que se consultan normalmente: Los usuarios (compradores) pueden consultar sus ordenes,  asi como el catalogo de productos en cualquier momento, a su vez el administrador de aplicaciones consulta frecuentemente las ordenes (compras) realizadas por los usuarios con el fin de iniciar el proceso de despacho. 

La actualizacion del listado de productos y su categoría se realiza de forma programada y autorizada por parte del Director de TI.

Flujos de datos normales (en cantidad, hora, frecuencia, origen de la consulta): 

<h2> Control ID.AM-6: Establecer roles y responsabilidades de Ciberseguridad</h2>


![Organigrama Empresa](https://user-images.githubusercontent.com/50051493/57118541-9ad13780-6d29-11e9-83f8-bb2df73a95de.PNG)

<p><strong>Director de TI:</strong></p>
<p>Supervisa la infraestructura de los sistemas de informaci&oacute;n dentro de la organizaci&oacute;n y es responsable de establecer los est&aacute;ndares de informaci&oacute;n para facilitar el control de la gesti&oacute;n de todos los recursos corporativos. El CIO tienen las siguientes responsabilidades:</p>
<p>&nbsp;</p>
<ul>
<li>Proporcionar asesoramiento y trabajar con miembros del equipo ejecutivo para identificar c&oacute;mo la tecnolog&iacute;a de la informaci&oacute;n puede ayudar a la compa&ntilde;&iacute;a a alcanzar sus objetivos de negocio y financieros. El Directorr de TI debe desarrollar una estrategia para alcanzar esos objetivos de la empresa, mejorando los procesos, aumentando la productividad de los empleados y mejorando la calidad de servicio al cliente.</li>
<li>Asegurar que la tecnolog&iacute;a de la informaci&oacute;n y la infraestructura de red sea compatible con las necesidades de computaci&oacute;n, procesamiento de datos y comunicaci&oacute;n de la compa&ntilde;&iacute;a. Un Director de TI debe reconocer y responder a las cambiantes necesidades de recursos de tecnolog&iacute;a, por ejemplo, tienen que desplegar infraestructura de red inal&aacute;mbrica y herramientas de colaboraci&oacute;n, como la videoconferencia de escritorio y los portales del proyecto.</li>
<li>Desarrollar pol&iacute;ticas de seguridad que protegen la infraestructura y los datos de la empresa, al tiempo que debe garantizar la privacidad de la informaci&oacute;n personal de los empleados.</li>
<li>Gestionar un equipo de especialistas en tecnolog&iacute;a de la informaci&oacute;n para manejar los recursos de IT de la empresa y apoyar a los usuarios departamentales. Si es necesario, un Director de TI organiza programas de formaci&oacute;n y certificaci&oacute;n para mejorar las habilidades del personal.</li>
<li>Satisfacer las necesidades de tecnolog&iacute;a de informaci&oacute;n de la empresa dentro de los l&iacute;mites presupuestarios, a menudo bajo presi&oacute;n para reducir los costos y mantener un alto nivel de servicio a los usuarios.</li>
</ul>
<p>&nbsp;</p>
<p><strong>Administrador de infraestructura:</strong></p>
<p>El administrador del sistema gestiona y mantiene el entorno de tecnolog&iacute;as de la informaci&oacute;n y las herramientas de gesti&oacute;n de operaciones, incluidas la administraci&oacute;n de los sistemas, la gesti&oacute;n de redes y las copias de seguridad. Normalmente, el administrador del sistema tambi&eacute;n mantiene diversos componentes e infraestructuras para reutilizarlas con otras soluciones.</p>
<p>&nbsp;</p>
<p><strong>Administrador de aplicaciones:</strong></p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><strong>Administrador de base de datos: </strong></p>
<p>El administrador de la base de datos (DBA) garantiza el rendimiento de los componentes relacionados con los datos, entre ellos, la seguridad de los datos y la disponibilidad de bases de datos. Su organizaci&oacute;n puede hacer referencia a este rol como DBA responsable de las operaciones, DBA de la empresa o DBA del almac&eacute;n de datos.</p>

<br> ROLES EN CIBERSEGURIDAD </br>

<p><strong>Oficial de Seguridad: </strong></p>
<p>Responsable del gobierno de seguridad y de impartir las directrices sobre los controles y políticas a implementar en sistemas de información y bases de datos.</p>

<p><strong>Operador de Monitoreo:</strong></p>
<p>Encargado de identificar, recibir, gestionar o reasignar alertas sobre la activcidad en sistemas de información y bases de datos.</p>

<p><strong>Analista de Seguridad:</strong></p>
<p>Responsable del apoyo en la implementaciónd e controles y poíticas, así como en gestión y soporte sobre bases de datos y sistemas de información.</p>

<p><strong>Analista de ciberseguridad:</strong></p>
<p>Responsable de la identificación de vulnerabilidades y ethical hacking sobre sistemas de información y bases de datos, así como de la respuesta a incidentes de seguridad informática.</p>

<h2>Control ID.GV-4: Procesos de Gobierno y Gesti&oacute;n para la identificaci&oacute;n de los riesgos de Ciberseguridad</h2>

<p> La gestión de Riesgos de Ciberseguridad se encuentra enmarcado dentro de las disposiciones de las Normas ISO 27001:2013, e ISO 31000:2018 y basado en las buenas prácticas a nivel internacional. </p>

![MetodologiaRiesgos](https://user-images.githubusercontent.com/50051518/57135673-ddb5fe00-6d6f-11e9-923e-a8ab166d40be.jpg)
