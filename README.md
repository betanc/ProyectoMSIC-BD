# ProyectoMSIC-BD
Proyecto materia seguridad en bases de datos MSIC

<b>CONTEXTO</b>: 

Empresa de E-commerce de venta de medicamentos en linea, utiliza tarjetas de crédito para los pagos, los cuales realiza a través de una plataforma externa. Los servidores están ubicados en Colombia en su propio datacenter y con administración propia. El datacenter no cumple con estándares TIER. (Incluir topología).
Si bien cuentan con responsabilidades asignadas para la toma de backups, no se cuenta con un procedimiento definido y estandarizado para ello.
El motor que la soporta es MySQL Community 8.0.16 bajo un servidor Debían. 
La plataforma web no fue creada utilizando metodologías de desarrollo seguro, no se han realizado análisis de vulnerabilidades en ninguna capa (aplicación web, servidor, base de datos).
No se realiza gestión ni monitoreo de logs en ninguna de las capas.

<b> Control ID.AM-2: Las plataformas y aplicaciones de software dentro de la organización están inventariadas</b>

Para implementar el control ID.AM-2,  se utiliza como marco de referencia informativa, principalmente los controles A.8.1.1, A.8.1.2 de la norma ISO/IEC 27001:2013. El resultado es el siguiente:

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
    <td class="tg-jpc1">Generalidades: Contiene 6 tablas que permiten a la organizacion desarrolar su core del negocio, la venta en linea de medicamentos a los usuarios registrados. <br>Motor: MySQL Community 8.0.16.<br>Tipo: Base de Datos Relacional.<br>Información sensible: Contiene datos personales y crediticios.<br>Licenciamiento del motor: GLP.<br>Puerto: 3306 <br>Tamaño: 51k</td>
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
</table>


<b> ID.AM-3: La comunicación organizacional y los flujos de datos están mapeados </b>

• Identificar y documentar los flujos de datos que son permitidos desde y hacia las bases de datos.

![Captura](https://user-images.githubusercontent.com/50051421/57111376-7a8d8280-6d01-11e9-9750-1b9376733d92.PNG)

Quienes son los administradores:
Desde donde se conectan
Datos se consultan normalment:
Flujos de datos normales: en cantidad, hora, frecuencia, origen de la consulta.




<b> Control ID.AM-6: Establecer roles y responsabilidades de Ciberseguridad</b>

Hemos usado el usuario “ root”,  que es el administrador, y que dispone de todos los privilegios de MySQL.

Para conservar la integridad de los datos y de las estructuras será conveniente que sólo algunos usuarios puedan realizar determinadas tareas, y que otras, que requieren mayor conocimiento sobre las estructuras de bases de datos y tablas, sólo puedan realizarse por un número limitado y controlado de usuarios.

No se pueden crear usuarios sin asignar al mismo tiempo privilegios, el crear un usuario se realiza principalmente por la necesidad de limitar las acciones que los usuarios pueden llevar a cabo. 

En MySQL podemos definir diferentes tipos de usuarios y asignar determinados privilegios.

Niveles de privilegios:


<table>
  <tr>
    <th><span style="font-weight:bold">Globales</span></th>
    <th>se aplican al conjunto de todas las bases de datos en un servidor. Es el<br>nivel más alto de privilegio, su ámbito es el más general.</th>
  </tr>
  <tr>
    <td><span style="font-weight:bold">De base de datos</span></td>
    <td>se refieren a bases de datos individuales, y por extensión, a todos los<br>objetos que contiene cada base de datos.</td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">De tabla</span></td>
    <td>se aplican a tablas individuales, y por lo tanto, a todas las columnas de esas tabla.</td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">De columna</span></td>
    <td>Es opcional y puede ser utilizado para especificar privilegios a cada columna. <br>Si los separamos por comas podemos poner una serie de lista de nombres<br>de columnas. (se aplican a una columna en una tabla concreta).</td>
  </tr>
  <tr>
    <td><span style="font-weight:bold">De rutina</span></td>
    <td>se aplican a los procedimientos almacenados.</td>
  </tr>
</table>
