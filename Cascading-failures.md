
Cacading failure:

    -  Vamos hablar sobre el fallo en cascada el cual es uno de lo mas importantes cuando hablamos de resiliencia.

    -  Una de las principales causas de este es cuando una parte del sistema experiemnta un fallo e inicia
    la destabilización del sistema mediante la porpagación del fallo.
    
        -   A menudo, esa propagación del fallo sigue el efecto mariposa, 
        donde una falla aparentemente pequeña puede generar un problema mucho mas grande evitando el correcto funcionamiento
        de todo el sistema.

        -   El mejor ejemplo para explicar este comportamiento es cuando la replica de un servicio falla y muere
        debido a una alto numero de peticiones, aumentando el numero peticiones en las replicas restantes y al 
        mismo tiempo la probabilidad de que las otras presenten el mismo fallo, causando un efecto domino
        sobre las todas las replicas de un servicio.

        -   En el siguiente diagrama tenemos un servicio con dos replicas procesando un total de 1200 peticiones 
        entre las dos. Si el servicio B por algún fallo deja de estar disponible, todas las peticiones seran enviadas
        a la siguiente replica la cual puede fallar de igual forma y las funcionalidades que entrega ese servicio ya
        no estaran disponibles.

    -  Otra cause que puede generar el fallo en cascada es el aogamiento de recursos, lo cual resulta en un
    Mayor latencia, elevado numero de error en el sistema en diferentes puntos.

        - Un punto importante aqui es que Dependiendo de qué recurso se agota en un servidor y 
        cómo se construye el servidor, el agotamiento de los recursos puede hacer que el servidor 
        sea menos eficiente o hacer que el servidor se bloquee.

        - Esto quiere que se pueden agotar diferentes tipos de recursos, 
        lo que resulta en efectos variables en los servidores.

        -  Uno de esos recursos es la CPU, donde si no hay suficiente CPU para manejar la carga de las
        solicitudes que ingresan al servidor, generalmente todsas las peticiones se vuelven lentas
        lo cual provoca alguno de los siguientes escenarios:

            -   Mayor número de solicitudes sin procesar o en vuelo y Colas de peticiones muy grandes.

            Debido a que las solicitudes tardan más en procesarse, 
            se manejan más solicitudes de manera simultánea 
            (hasta una capacidad máxima posible en la cual puede ocurrir 
            el encolamiento de peticiones con tiempos de espera mas altos). 

            Esto afecta a casi todos los recursos, incluida la memoria, el número de subprocesos activos , 
            el número de descriptores de archivo y los recursos de back-end, 
            y que por supuesto pueden tener otros efectos.


            - (Superar los tiempos definidos alas  peticiones de los clientes) Plazos de RPC perdidos 

            A medida que un servidor se sobrecarga, sus respuestas a los peticiones de sus clientes llegan más tarde, 
            lo que puede exceder los plazos establecidos por esos clientes. 
            Basicamente El trabajo que hizo el servidor  para responder la petición se pierde,
            existiendo un alta probabilidad de que los clientes hagan un nuevo intento, lo que puede llevar a una sobrecarga.

    
            - Reducir el beneficion de cache de la CPU.

            A medida que se usa más CPU, nucleos, resulta en un menor uso de cachés locales 
            y una menor eficiencia de la CPU.

        - Memoria
        - El segundo recuso importante es la Memoria, la cual debido a algunos de los anteriores escenarios,
        su uso puede aumentar, por ejemplo cuando hay encolomaento de peticiones y el agotamiento de memoria
        puede causar los siguientes escenarios:

            -   Dying task, la cual es cuando el administrador de contenedores o la maquina virtual, puede
            deshalojar una tarea por exceder el limite de recursos disponibles o cuando bloqueos en la
            aplicación se puede provacar la perdida de tareas.

            -   El aumento de las ejecuciones del Garbage collector en Java, lo cual resulta en un mayor uso de CPU.

            En este escenario se puede presentar el siguiente comportamiento o un circulo vicioso, 
            Hay menos CPU disponible, 
            lo cual resulta que las peticiones sean mas lentas, 
            lo que ocaciona en un mayor uso de RAM,
            lo que resulta en mas ejecuciones del Garbage collector.
            Y este comportamiento es conocido como la espiral de muerte del Garbage collector “GC death spiral.”

            -   Y el ultimo es el aumento de subprocesos

            Si el servidor agrega subprocesos según sea necesario, la sobrecarga de subprocesos puede usar demasiada RAM,
            y en casos extremos, el thread starvation puede hacer que se quede sin ID de proceso.


        - Por ultimo la indisponibilidad de servicios por agotamiento de recursos

        En este caso el agotamiento de recursos puede provocar el bloqueo de los servidores, 
        por ejemplo un servidor puede fallar cuando superan el limite de RAM y una vez que un 
        par de servidores se bloqueen por sobrecarga, la carga en los servidores restantes puede aumentar
        y provocar que también lleguen a un punto de bloqueo.
        
        y es aqui donde sucede el problema, a menudo es difícil escapar de este escenario porque tan pronto como 
        los servidores vuelven a estar en línea son bombardeados con una tasa extremadamente 
        alta de solicitudes y fallan casi de inmediato.


Bulkhead:

    - Es la analogia de un barco donde se previene que el mismo se hunda cuando el barco sufre algún daño
    en el caso tal de no tener las separaciones del barco se hundiria, los bulkhead establece la separación
    adecuada para evitar que el agua llegue a los demas comportamientos

    - Lllevando el concepto un poco mas a temas de negocio, tenemos el ejemplo donde Netflix o cualquier comercio
    envio un alto numero de transacciones sobre un solo tipo de operación, existiendo la posibilidad de que por algun 
    motivo ese alto numero de peticiones concurrentes excedan el limite del servicio, ocacionado que otra tipos
    de operaciones no sean procesadas. Debido a que no hay hilos para procesarlas.

    - ¿Como reaccionaria el Bulkhead?... En este caso el servicio tendria cubierto cada método con un blukhead el
    limitaria el numero de peticiones para cada tipo de operación, con el objetivo de afectar las otra operaciones
    del servicio.

    - En pocas palabras el Bulkhead es un limitador opraciones concurrentes o paralelas y basicamente como 
    observamos en la imagen, se define que solo es permitido ejecutar 5 llamadas concurrentes y las demas seran 
    encoladas durante el tiempo que se defina en la configuración, el valor por default 0, el cual permite un fallo rapido.



Chaos engineering is the discipline of experimenting on a distributed System in order to build confidence 

Chaos engineer:

    -  Chaos enigneer es la disciplina de experimentar sobre un sistema distribuido con el objetivo 
    de construir confianza en la capacidad del sistema para soportar diferentes comportamientos o condicionese
    en ambiente productivo, abordando directamente la disponibilidad del sistema.

    En otras palabras, el enfoque es encontrar problemas antes de que sean experimentamos por los verdaderos 
    usuarios del sistemas.


    - Principles:
        -   Construir una hipotesis sobre el estado estable del sistema:
            
            - Basicamente, habla sobre que nos debemos concentrar el resultado medible de un sistema,
            en lugar de los atributos internos del sistema.
            Por ejemplo, las tasas de error, los percentiles de latencia, el rendimiento general del sistema
            y en entre otros que pueden ser metricas de interes que representan un comportamiento
            estable estable del sistema.

            Esto con el objetivo de que el experimento se enfoque en el que sistema funcione y
            no en tratar de validar como funciona.

        - Variar lo eventos del mundo real

            - Este principio se basa en que el caos debe reflejar eventos del mundo real.
            Lo que se busca es que se prioricen los eventos por el potencial de impacto o frecuencia del 
            escenario.

            Por ejemplo, fallas del hadware, fallas de software respuestas mal formadas.
            Cualquier evento capaz de interrumpir el estado estable del sistema.

        - Ejecutar experimentos en producción

            - Usualemente, Los sistemas se comportan de manera diferente según el entorno 
            y los patrones de tráfico. Asi que por esta razón uno de los principios
            de chaos engineer es que la mayoria de casos prefier experimentar 
            directamente en el trafico de producción.

            - Generar Cultura.

        - Automatizar y ejecutar continuamente los experimentos.

            -   Ejecutar algunos experimentos requiere mucha mano de obra,
            por tal razón es  necesario la automatización y ejecutarlos continuamente para
            garantizar que el sistema sigue cumpliendo las condiciones para seguir disponible.
