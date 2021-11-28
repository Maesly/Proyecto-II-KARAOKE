## Documento ejecutivo

El presente documento consiste en un resumen ejecutivo del proyecto Karaoke, para este proyecto existe previamente una primera versión que básicamente trata de una página web desde la cual permite a los usuarios registrarse y acceder a su página de inicio. Dentro de la página web, el usuario es capaz de navegar a través de una lista de canciones de su preferencia, pero también la misma permite navegar en busca de más canciones para ser añadida a la lista de reproducción del karaoke del usuario. Cabe destacar que al tratarse de un karaoke, una vez seleccionada la canción es posible para el usuario pausar y reproducir la música escogida para cantar.
 La plataforma de la primera versión se encuentra construida con base a una arquitectura monolítica debido a los requerimientos establecidos y necesarios para la aplicación. Sin embargo,  luego de lanzada la aplicación el equipo de trabajo realiza mantenibilidad de la aplicación en busca de mejoras para la misma, encontrando con ciertas debilidades que pueden ser mejoradas en una nueva versión de la aplicación. A lo largo del documento se explicarán cada una de las partes donde se encontró una debilidad, cuál era el alcance previo de la aplicación en su primera versión, así como el plan de mejora que se siguió para mejorar la experiencia de Karaoke.

### Índice


```markdown
1. Análisis de debilidades de su arquitectura
2. Límites de su aplicación
3. Plan de mejora
4. Nuevos features

```

### Análisis de debilidades de su arquitectura
Si bien la versión 1.0 de Karaoke! fue todo un éxito, esto no quita el hecho de que haya cosas que se deben mejorar, esto con el fin de poder brindarles a los usuarios un mejor servicio y una mejor experiencia; además, si se crean nuevas mejoras, esto puede atraer a nuevos usuarios que hagan uso de la aplicación, logrando que haya un auge mayor e incremente la popularidad de Karaoke!. Ahora bien, lograr este objetivo presenta una serie de nuevos retos que se deben tomar, un análisis objetivo y tomar decisiones que sean del mayor beneficio para la usabilidad y estabilidad de la aplicación. 
De entrada una de las desventajas que se tenía era que la aplicación fue basada en una arquitectura monolítica, que si bien se encontraban ventajas como una implementación simple y un bajo costo de empleo, para los planes a futuro ya no era lo suficientemente conveniente, pues para los propósitos o implementaciones que se le querían agregar a la aplicación, el uso de esta arquitectura presenta debilidades o desventajas, tales como una escalabilidad deficiente y un ciclo largo de reparación en línea, que a largo plazo iban a tener un coste mayor para el sistema. 
Tomando en cuenta lo anterior, se concluyó en que la mejor decisión para los planes que se tenían en mente y que se querían realizar, la aplicación debía apoyarse en una arquitectura basada en microservicios, pues presenta una serie de ventajas que se acoplan o van muy de la mano con las intenciones del proyecto, las cuales serán abordadas más adelante. 
Como en la gran mayoría de aplicaciones, puede haber una serie de falencias, que, si bien muchas veces no representan un gran riesgo, lo más conveniente es poder abordarlas con el fin de mejorarlas o erradicarlas, para brindar una aplicación de mayor confianza para los usuarios, entre las posibles falencias a mencionar que se podrían presentar en la aplicación Karaoke!, se encuentran las siguientes: 
- Seguridad: si bien se dispone del uso de Keycloak, el cual brinda confianza en cuanto al manejo del inicio de sesiones, esto no implica que no se deba de usar alguno otro tipo de protocolo o de encriptación con el fin de que de no ocurran amenazas o violaciones a la privacidad de los usuarios y su información.
- Alta disponibilidad: poca disponibilidad, ya que cualquier error puede hacer que todo el sistema se bloquee y no se preste ningún servicio.
- Mantenibilidad: debido a la arquitectura con que se cuenta, la mantenibilidad es muy baja, ya que su modularidad implica que cualquier cambio tiene un gran impacto en el sistema; además, siguiendo esta línea, tiene muy poca posibilidad de ser modificado de forma efectiva y eficiente sin introducir defectos o degradar el desempeño.
- Desplegabilidad: arranque lento del sistema, pues hay muchos módulos de arranque involucrados, lo que resulta en un largo período de arranque del sistema.
- Escalabilidad: La escalabilidad es compleja, ya que está supeditada a una infraestructura rígida que depende de un conjunto de recursos finito, por lo que el suponer un crecimiento para la aplicación no sería tarea fácil por todas las variables que se involucran y su ensamble tan riguroso.

### Límites de su aplicación

El sistema diseñado y creado, tiene muchas falencias, las cuales tan siquiera se puede contabilizar, pues aunque se realizaron algunos de los features que se requerían, estos no fueron realizados a cabalidad, por lo que hablar sobre métricas que impliquen cuántos usuarios concurrentes máximos soporta la aplicación, o bien, mediciones sobre el tiempo de respuesta en las consultas antes de que se tarden al saturar la base de datos y conocer cuánto es el máximo de datos, fueron imposibles para el presente documento, por lo que mostrar algún aproximado o un dato sería algo muy alejado de la realidad. 

### Plan de mejora

Como se mencionó anteriormente en este documento, la arquitectura escogida para los nuevos planes del sistema es una basada en microservicios, la cual tiene tanto sus ventajas como desventajas que mencionaremos a continuación:
## Ventajas
```markdown
    - [] Modularidad: al tratarse de servicios autónomos, se pueden desarrollar y desplegar de forma independiente.  Además, un error en un servicio no debería afectar la capacidad de otros servicios para seguir trabajando según lo previsto.
    - [] Escalabilidad: como es una aplicación modular, se puede escalar horizontalmente cada parte según sea necesario, aumentando el escalado de los módulos que tengan un procesamiento más intensivo.
    - [] Versatilidad: se pueden usar diferentes tecnologías y lenguajes de programación, lo que permite adaptar cada funcionalidad a la tecnología más adecuada y rentable.
    - [] Rapidez de actuación: el reducido tamaño de los microservicios permite un desarrollo menos costoso, así como el uso de “contenedores de software”, como Docker, permitiendo que el despliegue de la aplicación se pueda llevar a cabo rápidamente.
    - [] Mantenimiento simple y barato: al poder hacerse mejoras de un solo módulo y no tener que intervenir en toda la estructura, el mantenimiento es más sencillo y barato.
    - [] Agilidad: se pueden utilizar funcionalidades típicas (autenticación, trazabilidad, etc.) que ya han sido desarrolladas por terceros, por lo que no hace falta o no es necesario que se tengan que crear, un ejemplo de ello para este proyecto es el uso de dashboard para presentar estadísticas.
```
## Desventajas 
``` markdown
    - [] Alto consumo de memoria: al tener cada microservicio sus propios recursos y bases de datos, consumen más memoria y CPU.
    - [] Inversión de tiempo inicial: al crear la arquitectura, se necesita más tiempo para poder fragmentar los distintos microservicios e implementar la comunicación entre ellos.
    - [] Complejidad en la gestión: si contamos con un gran número de microservicios, será más complicado controlar la gestión e integración de estos, por lo que resulta necesario disponer de una centralización de trazas y herramientas avanzadas de procesamiento de información que permitan tener una visión general de todos los microservicios y orquesten el sistema.
    - [] No uniformidad: aunque disponer de un equipo tecnológico diferente para cada uno de los servicios tiene sus ventajas, si no se gestiona correctamente, conducirá a un diseño y arquitectura de aplicación poco uniforme.
    - [] Dificultad en la realización de pruebas: debido a que los componentes de la aplicación están distribuidos, las pruebas y test globales son más complicados de realizar.
    - [] Coste de implantación alto: una arquitectura de microservicios puede suponer un alto coste de implantación debido a costes de infraestructura y pruebas distribuidas.
```
El plan de migración que mejor conviene para el proyecto es una basada en una migración de datos por goteo o por fases, ya que usando este tipo de el sistema antiguo y el nuevo se ejecutan en paralelo durante la implementación, lo que elimina el tiempo de inactividad o las interrupciones operativas, lo cual es muy conveniente dado el fin que tiene el sistema, siendo así que los procesos que se ejecutan en tiempo real pueden mantener los datos en continua migración. Los pros de este enfoque son que es menos propenso a fallos inesperados y no requiere tiempo de inactividad, pero entre las desventajas de este enfoque son que es más caro, lleva más tiempo y requiere esfuerzos y recursos adicionales para mantener dos sistemas en funcionamiento. Este tipo de migración es ideal para sistema, como el presente, donde no es bueno que exista un tiempo de inactividad prolongado, pues parte de los planes es que haya un crecimiento a nivel de usuarios, lo cual no hubiera pasado si la plataforma presentara fallos o no estuviera funcional en su totalidad. 
Como parte de los cambios que se quieren realizar, se tiene que realizar un tipo de plan o camino a seguir para poder generar los nuevos features, dichas actividades son las siguientes: 
1. Iteración 1
     - Como gerente, quiero que la información del sistema se encuentre en la nube
       - Migrar la información de los usuarios 
       - Migrar la información de las canciones
2. Iteración 2
     - Como usuario, quiero poder obtener una calificación de la canción que cante
       - Mostrar la letra de la canción
       - Grabar la voz del usuario cantando
       - Parsear la grabación a un archivo de texto mediante el uso de un API 
       - Comparar lo cantado con la letra
       - Crear una métrica para obtener una puntuación
       - Mostrar la puntuación obtenida
3. Iteración 3
    - Como usuario, quiero poder observar información del artista o grupo 
      - Obtener información del artista mediante un API 
      - Ordenar y filtrar la información del artista
      - Desplegar la información obtenida mientras se reproduce la canción
4. Iteración 4
    - Como usuario, quiero poder observar estadísticas sobre mi cuenta 
      - Desplegar la información del usuario 
      - Filtrar canciones reproducidas por el usuario
      - Mostrar lista de las canciones reproducidas 
      - Mostrar artistas favoritos
      - Hacer un recuento de las palabras con mayor y menor dificultad 
      - Mostrar el recuento de las palabras 

## Nuevos features

Una vez determinadas las debilidades del sistema de karaoke y generado el plan estratégico para mejorar las mismas, se determina que aprovechando la nueva versión se añadirán algunas características más con el fin de proporcionar una mejor experiencia en la página web, y a su vez enriquecer el sistema con más posibilidades para los usuarios. Las características que se pretende añadir son las siguientes:
### Puntuación
La finalidad de un Karaoke es divertirse durante el transcurso de la canción, sin embargo también es importante para el usuario saber que tal lo hizo o qué tanto porcentaje de la letra pudo cantar correctamente. Es por esto por lo que para proporcionarle una mejor experiencia al usuario con la aplicación de Karaoke se decide añadir una estadística para puntuar o calificar cuál fue su desempeño del usuario en el karaoke. Más precisamente, en cuanto a implementación, el equipo decide hacer uso de un microservicio siguiendo la línea del plan de mejora que sea capaz de proporcionar una puntuación al usuario acerca de cuántas coincidencias hace con respecto a la letra original de la canción seleccionada.
### Información del artista
Para esta nueva actualización de la aplicación, se decide colocar en la información acerca del artista de manera accesible para el usuario. Esto se añade como una nueva característica debido a que en algunos casos el usuario canta la canción y no sabe la información acerca del artista, entonces debe buscar dicha información fuera de aplicación, es por esto por lo que se le adjunta dicha información como un plus a la aplicación para lograrla hacer mucho más atractiva para el usuario.
### Estadísticas
Cómo parte de los nuevos elementos contemplados para la versión 2.0 de karaoke, se añaden estadísticas propias de cada usuario a su perfil con el fin de mostrarle su desempeño y demás información en la aplicación. En el fin u objetivo de realizar dicho feature es mostrarle al usuario de una manera sencilla, compacta y agradable las estadísticas sobre sus canciones favoritas, así como de sus artistas favoritos, y también de aquellas palabras más difíciles de pronunciar para el usuario en un top 10 mostrado por medio de un Dashboard.


