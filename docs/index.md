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

