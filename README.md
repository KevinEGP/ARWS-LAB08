# ARWS_Scalability_lab

## Parte 1

Punto 12: Este modelo de escalabilidad no ofrece la capacidad de rendimiento suficiente pues como se evidecia en la información a continuación, el rendimiento obtenido con una maquina mucho más potente que la inicial, no dió un rendimiento proporcinalmente superior.

#### Preguntas

1. ¿Cuántos y cuáles recursos crea Azure junto con la VM?

Se crea el recurso de la maquina virtual, una interfaz de red, una dirección ip publica, un grupo de seguridad en la red y una red virutal.

2. ¿Brevemente describa para qué sirve cada recurso?

Maquina virtual es un equipo de computo virtualizado, <br>
Interfaz de red: permite conectarse a los recursos de internet.<br>
IP address publica: Es la dirección que permite identficar al dispostivo en la red. <br>
Grupo de seguridad de la red: Es similar a un firewall para proteger los recursos. <br>
Red virtual: Es una red virtualizada que conecta a los recursos. <br>

3. ¿Al cerrar la conexión ssh con la VM, por qué se cae la aplicación que ejecutamos con el comando npm FibonacciApp.js? ¿Por qué debemos crear un Inbound port rule antes de acceder al servicio?

Se cierra porque este proceso se ejecuta en la instancia de la terminal por la que nos conectamos y al desconectarnos esta instancia desaparece. Se debe crear el puerto de entrada para que el proceso sea visible y accesible desde otros dispositivos.

4. Adjunte tabla de tiempos e interprete por qué la función tarda tando tiempo.

B1ls <br>
1000000 => 31.70 s <br>
1010000 => 31.06 s <br>
1020000 => 26.25 s <br>
1030000 => 30.65 s <br>
1040000 => 29.53 s <br>
1050000 => 29.86 s <br>
1060000 => 30.92 s <br>
1070000 => 29.52 s <br>
1080000 => 31.69 s <br>
1090000 => 35.81 s <br>
B2ms <br>
1000000 => 21.55 s <br>
1010000 => 21.16 s <br>
1020000 => 22.25 s <br>
1030000 => 23.21 s <br>
1040000 => 24.45 s <br>
1050000 => 25.58 s <br>
1060000 => 25.99 s <br>
1070000 => 26.11 s <br>
1080000 => 26.66 s <br>
1090000 => 27.11 s <br>

Tarda demasiado tiempo porque no tiene ningun tipo de memoria sino que debe calcular cada iteración nuevamente

5. Adjunte imágen del consumo de CPU de la VM e interprete por qué la función consume esa cantidad de CPU.

B1ls <br>
![image](https://user-images.githubusercontent.com/60078276/144887220-b5be21b0-c32c-499e-9857-f6077872917b.png)

B2ms <br>
![image](https://user-images.githubusercontent.com/60078276/144911322-2a6c7091-c286-4547-972b-8ddf8c3ddc14.png)

Dado que debe calcular en cada instante toda la recurrencia sin memorizar, el CPU se utiliza al máximo

6. Adjunte la imagen del resumen de la ejecución de Postman. Interprete:

Tiempos de ejecución de cada petición.

![image](https://user-images.githubusercontent.com/60078276/144922036-50f6b4fd-bba7-4fd9-b0b4-fa8f286b57dd.png)



Si hubo fallos documentelos y explique.

![image](https://user-images.githubusercontent.com/60078276/144922130-0b97d732-979f-41db-8141-16c5103c6df7.png)



7. ¿Cuál es la diferencia entre los tamaños B2ms y B1ls (no solo busque especificaciones de infraestructura)?

B2ms ofrece un rendimiento maximo del doble en comparación a B1ls, pero con en su rendimiento base, B2ms tiene 5x más rendimiento que B1ls. Además, el precio por hora aumeta casi 9x.

8. ¿Aumentar el tamaño de la VM es una buena solución en este escenario?, ¿Qué pasa con la FibonacciApp cuando cambiamos el tamaño de la VM?

No es una buena opción en relación al precio y al rendimiento. La funcion tiene más cores para ejecutarse en paralelo.

9. ¿Qué pasa con la infraestructura cuando cambia el tamaño de la VM? ¿Qué efectos negativos implica?

El principal efecto negativo es el precio, pues pasa de $0.0144/hour a $0.0912/hour y esto a gran escala sería un problema precisamente de escalabilidad.

10. ¿Hubo mejora en el consumo de CPU o en los tiempos de respuesta? Si/No ¿Por qué?

Sí, en promedio demoró 10 segundos menos cada ejecuciión pero el porcentaje de uso de CPU fue similar.

11. Aumente la cantidad de ejecuciones paralelas del comando de postman a 4. ¿El comportamiento del sistema es porcentualmente mejor?

No, dado que son ejecuciones independientes entre ellas, el comportamiento es similar.


## Parte 2

1. ¿Cuáles son los tipos de balanceadores de carga en Azure y en qué se diferencian?, ¿Qué es SKU, qué tipos hay y en qué se diferencian?, ¿Por qué el balanceador de carga necesita una IP pública?

Load Balancer estándar: Se encarga de equilibrar la carga del tráfico de la capa de red, enruta el tráfico dentro de las regiones y entre ellas.
Gateway Load Balancer: Permite encadenamiento de servicios, como análisis, DDoS en línea, firewall, etc.
Load Balancer básico: Para las aplicaciones a pequeña escala que no necesitan alta disponibilidad o redundancia.

2. ¿Cuál es el propósito del Backend Pool?

Backend pools: Son un conjuntos de servidores a los que se redirige el tráfico si se cumple alguna de las reglas establecidas.

3. ¿Cuál es el propósito del Health Probe?

Health Probe: Permite idnetificar cuales de l os servidores del backend pool están activos.

4. ¿Cuál es el propósito de la Load Balancing Rule? ¿Qué tipos de sesión persistente existen, por qué esto es importante y cómo puede afectar la escalabilidad del sistema?.

Las Load Balancing Rule permiten configurar el tráfico al que se envía a al Backend Pool, de tal forma que se filtre para algunos de estos servdores.

5. ¿Qué es una Virtual Network? ¿Qué es una Subnet? ¿Para qué sirven los address space y address range?

Permite a muchos recursos de Azure comunicarse de forma segura entre usuarios, con Internet y con las redes locales.

6. ¿Qué son las Availability Zone y por qué seleccionamos 3 diferentes zonas?. ¿Qué significa que una IP sea zone-redundant?

Las Availability Zone son secciones en las que se dividen fsicamente los recursos y son independientes para evitar fallos de software o hardware. Las IP zone-redundant significa que están estna dentro de una Availability Zone que tiene 3 zonas activas. 

8. ¿Cuál es el propósito del Network Security Group?

Son reglas de seguridad que filtran el trafico hacia los recursos de Azure, pare denegar tráfico no deseado dentro de una red virtual Azure.

9. Informe de newman 1 (Punto 2)

Balanceo de carga con 3 VM y 2 Peticiones concurrentes

![Screenshot from 2021-12-06 18-31-32](https://user-images.githubusercontent.com/60078276/144948914-6f0cf50e-4d37-4325-8722-1a5145ca7f5d.png)


Balanceo de carga con 4 VM y 4 peticiones concurrentes

![Screenshot from 2021-12-06 18-50-00](https://user-images.githubusercontent.com/60078276/144949049-be072790-3b8b-4d3d-81e1-ca2333cee564.png)

![Screenshot from 2021-12-06 18-50-06](https://user-images.githubusercontent.com/60078276/144949134-6f8474f9-40ae-4c08-8301-20f467d727dd.png)

![Screenshot from 2021-12-06 18-50-09](https://user-images.githubusercontent.com/60078276/144949153-345851d4-4e3a-487b-aaf4-4222773a983f.png)



10. Presente el Diagrama de Despliegue de la solución.

![Load_Balancing drawio](https://user-images.githubusercontent.com/60078276/145038928-b3b49818-da4e-480f-a8d8-f1d54d531fc9.png)

