# Unidad 8
## Registros
Un registro es una memoria de alta velocidad que le sirve al programador de aplicaciones para llevar a cabo sus tareas.
Los registros se clasifican en cuatro grupos grandes:
1. **Registros de proposito general**
2. **Registro de puntero de instruccion**
3. **Registro de estado o de Señalizadores**
4. **Registros de Segmento** 

### Registros de proposito general 
Este grupo consta de ocho registros capaces de trabajar con informacion de 32 bits cuando se aprovecha todo su tamaño aunque tambien puede manejar datos de 16 bits. Los registros de proposito general pueden manejar tanto datos como direcciones. En el caso de que se almacene una direccion en el mismo, sera el desplazamiento de una direccion de memoria.
Estos registros son:
- EAX: **Acumulador**
- EBX: **Base**
- ECX: **Contador**
- EDX: **Datos**
- ESP: **Puntero Pila**
- EBP: **Puntero Base**
- ESI: **Indice Fuente**
- EDI: **Indice Destino**

Para acceder a los registros en 16 bits se utiliza su nombre sin la "E" de extended. 
![](https://dt5vp8kor0orz.cloudfront.net/3c8ae9feb797c54375ea905e2612079db3e327ce/28-Figure3-5-1.png)
#### Acumulador
Es un registro que se emplea en todas las operaciones Aritmetico-Logicas. Los procesadores utilizan mucho el accumulador debido a que por una parte contienen el operando y por otra se carga con el resultado de las operaciones de la ALU.
#### Base
Contiene una direccion que apunta la base de un conjunto de dato. La longitud de las direcciones dependiendo el procesador que se este utilizando puede variar lo cual hace que en casos como el 8086 se utilize el registro en 16 bits y como el caso del pentium se utilice con 32 bits. 
#### Contador 
Se carga el numero de veces que se ejecuta una operacion. Sirve mucho para los bucles
#### Datos 
Se emplea para almacenar las direcciones de los puertos de entrada y de salida en las instrucciones que manejan I/O.
#### Puntero Pila y Puntero Base 
Sirven para controlar el direccionamiento en la pila. 
Los tres registros encargados de realizar operaciones en la pila son los siguientes
- **Registro de Segmento de pila (SS)**. Contiene un puntero a la ubicacion del segmento de pila
- **Registro Puntero de pila (ESP)**. Contiene el desplazamiento del la cima de la pila en el segmento de la pila actual. Cuando se introduce un elemento en la pila, el procesador decrementa el puntero ESP y escribe el elemento en la cima de la pila. Cuando se saca un elemento de la pila se hace la operacion inversa.
- **Registro puntero base de la pila (EBP)**. Se utiliza para acceder a estructuras de datos pasadas a la pila. Cuando el segmento EBP se utiliza para direccionar memoria, el segmento de pila es referenciado. Este registro apunta a la base de la pila y cuando existen rutinas hace el papel de ESP para no modificar el valor de este ultimo.

#### Indicie fuente y Indice destino
Son dos punteros de direcciones necesarios para trabajar con la cadena las cadenas de caracteres. Las instrucciones que realizan operaciones entre los elementos de las cadenas que se aplican a una cadena fuente y una cadena destino, cada una de ellas esta direccionada por los registros ESI y EDI. 

### Registro puntero de instrucciones EIP
El registro EIP es el puntero de las instrucciones o contador del programa y no esta disponible para el programador, lo gobierna implicitamente el flujo de control de las instrucciones, las interrupciones o excepciones. 

Este registro puede trabajar en dos modos:
1. Modo nativo o protegido: Tiene una logitud de 32 bits y recibe el nombre de EIP. Almacena el desplazamiento que hay que añadirle a la base del segmento de codigos para obtener la direccion donde esta la siguiente instruccion a ejecutar. El valor maximo del desplazamiento en el segmento sera de 4gb.
2. Modo real: Tiene una longitud de 16 bits y recibe el nombre de IP. Nuevamente contiene un dezplazamiento que hay que añadirle a la base del segmento de codigos para obtener la direccion donde esta la siguiente instruccion. El valor maximo del desplazamiento en el segmento sera de 64KB.

### Registro de estados EFLAGS
Este registro consta de 32 bits de los cuales la mayoria son señalizadores de estado controlados por la ALU y actuando los restantes como señalizadores del sistema ligados a recursos de los cuales dispone el sistema.
![](https://grandidierite.github.io/assets/img/eflags.png)
Descripcion de bits:
1. CF: Señalizador de acarreo en el bit de mas peso al realizar una operacion aritmetica.
    - 0: No ocurrio acarreo en la operacion.
    - 1: Ocurrio acarreo en la operacion
2. PF: Bit de paridad impar.
    - 0: Valor para generar paridad impar. 
    - 1: Toma este valor para generar pariedad par en los resultados.
3. AF: Señalizador de acarreo auxiliar
    - 0: En caso de no ocurrir acarreo en el bit 3 el resultado
    - 1: Toma este valor cuando ha ocurrido accarreo en el bit 3 del resultado. Se utiliza en las operacione del BCD.
4. ZF: Señalizador de cero
    - 0: Cuando alguno de los bits de resultado es uno.
    - 1: Cuando todos los bits de resultado son cero. 
5. SF: Señalizador de signo
    - 0: Si el bit de mas peso del resultado de la operacion es 0.
    - 1: Si el bit de mas peso del resutlado de la operacion es 1.
6. TF: Excepcion al terminar la ejecucion de una instruccion.
    - 0: No hay excepciones de depuracion al terminar cada instruccion.
    - 1: Provoca una excepcion al completarse la ejecucion de la instruccion en curso.
7. IF: Flag de habilitacion de las instrucciones enmascarables. 
    - 0: Prohibe el reconocimiento de las interrupciones externas e ignora las peticiones de las interrupciones enmascarables.
    - 1: Permite el reconocimiento de las instrucciones enmascarables lanzadas atravez de la patita de INTR.
8. DF: Flag de direccion de exploracion de las cadenas de caracteres o strings.
    - 0: Postincremento automatico de ESI y EDI
    - 1: Postdecremento automatico de los registros ESI y EDI que direccionan la cadena.
9. OF: Flag de overflow
    - 0: Si no existe overflow
    - 1: Vale uno si el resultado es erroneo.
10. IOPL: Nivel de privilegio de las entradas y salidas 
11. RF: Flag de reanudacion. Su activacion provoca la ejecucion de la siguiente instruccion cuando se produce una excepcion en una instruccion.
    - 0: No se ignoran los puntos de parada.
    - 1: Se ignoran los puntos de depuracion o de parada.
12. VM: Modo Virtual. Mediante este bit, se permite el paso de modo protegido a modo virtual. 
    - 0: No hay paso al modo virtual 86. 
    - 1: Estando en modo protegido se pasa al modo virtual 86. 
13. AC: Bit de checkeo de alineamiento.
    - 0: Ignora el desalineamiento.
    - 1: Se produce una excepcion cuando encuentra algo desalineado en la memoria. 
14. VIF: Realiza la misma tarea que el IF pero en modo virtual.
15. VIP: Interrupciones pendiente en modo virtual.
    - 0: No hay interrupcion pendiente.
    - 1: Interrupcion mascarable pendiente.
16. ID: Bit de indentificacion. Informa si el procesador soporta la instruccion CPUID que sirve para su identificacion.
    - 0: No soporta la instruccion. 
    - 1: Soporta CPUID. 
### Registros de Segmento
Para hablar de los registros de segmentos primero hay que definir lo que es un segmento. Un segmento es un trozo de memoria que contienen un mismo tipo de informacion. Existen tres tipos de segmentos disponibles para el programador de aplicaciones:
1. **Segmento de pila**
2. **Segmento de codigo**
3. **Segmento de datos**

El procesador controla en cada instante seis segmentos a los que referencia a traves de los registros de segmento.
La memoria esta formada por una informacion que consta de los siguientes campos:
1. Selector: Son los 14 bits de mas peso del registro que referencia al segmento al que se quiere acceder y con ello se encuentra la base donde comienza el segmento, el limite o tamaño que tiene sus atributos. 
2. Desplazamiento: El valor que se añade a la base del segmento para localizar la direccion que hay que acceder en él.

Estos son los siguientes registros de segmento:
1. CS: El registro CS, contiene en cada momento la informacion necesaria del segmento de instrucciones que esta ejecutando la CPU, es decir, el segmento en curso. El desplazamiento que hay que añadirle a la base para obtener la direccion de un dato dentro de este segmento proviene del registro EIP.
2. SS: El registro SS, guarda el valor del selector del segmento de pila en curso. El registro ESP contiene el desplazamiento que debe añadirse a la base del segmento de pila para la cima por donde se cargan y descargan los datos.
3. DS: El registro DS, soporta el valor del selector del segmento de datos y el desplazamiento viene especificado en el modo de direccionamiento utilizado por la instruccion para expresar operandos o resultados.

#### Segmentacion en modo real 
Cuando se trabaja en modo real un segmento queda definido por:
- Base: La direccion de comienzo de 20 bits.
- Desplazamiento: De tamaño de 16 bits.

En modo real todos los segmentos estan especificados por una direccion logica compuesta por dos campos de 16 bits cada uno. 
- Selector: Referencia a la base del segmento, la cual se deduce a partir del valor contenido en el registro de segmentos apropiado. 
- Desplazamiento: Referencia nuevamente a los 16 bits de desplazamiento.

El calculo final quedaria así:
![alt text](image-2.png)
Donde RS seria el segmento al que queremos ingresar.

#### Segmentacion en modo protegido
Cuando un procesador trabaja en modo protegido, un segmento queda caracterizado por tres parametros fundamentales que son comprobados automaticamente por el sistema de proteccion cada vez que se utiliza. Estos son:
1. Base: Direccion lineal donde comienza el segmento. Esta formado por 32 bits que es la longitud en la memoria fisica que puede alcanzar un tamaño maximo de 4 GB
2. Limite: Consta de 20 bits que determinan con exactitud el tamaño total del segmento usado por el programador y en el que reside informacion valida. 
3. Atributos: se trata de un campo de 12 bits que proporciona las caracteristicas relevantes del segmento como
    - Tipo de segmento, admitiendo la variante de lectura, estrictura, ejecutable o la combinacion de alguno de estos.
    - Nivel de privilegio, que oscila entre 0 y 3. Es el grado de seguridad que tiene el contenido del segmento del sistema.
    -  Indicador de presencia para saber si se encuentra en la memoria vitual o hay que ir a buscarlo. 

Todos estos datos se encuentran dentro de una estrucura llamada descriptor de segmentos que ocupa 64 bits.
Estos descriptores de segmento se encuentran dentro de una tabla llamada "tabla de descriptores" la cual se ubica en la memoria principal. 

## Pila 
### Segmento de pila
Zona en memoria de tamaño variable destinado a almacenar o a agrupar mediante el criterio de datos referenciados a la pila para determinadas instrucciones y procesos de ejecucion. 
### Estructura de la pila
La pila es una estructura de datos de tipo LIFO donde el primer elemento en entrar es el primero en salir. 
### Registros asociados
- SS (Registro segmento de stack)
- SP (Registro puntero de pila)
- BP (Registro puntero base)

### Funciones basicas
- Almacenar la direccion de retorno del IP y, eventualmente, el CS cuando ocurre una llamda a un procedimiento, tambien conocido como subrutina.
- Almacenar el estado del procesador cuando se produce una interrupcion. Los registros que obligatoriamente apila son el CS, el IP y el estado de los flags. 
- Pasar parametros a los procedimientos.

El medio por el cual se accede a la pila es por los registros punteros SP y BP, dode SP contiene la direccion de la cima de la pila. Es decir, CS:SP.

La escritura o lectura de datos de la pila es un procedimiento de software y se realiza decrementando e incrementando el SP. 

La encargada de acceder a la pila es la CPU, ejecutando dos tipos de instrucciones que son:
- PUSH: Decrementa el valor del SP y luego almacena la palabra en la pila. 
- POP: Extrae una palabra de la pila y desafecta las pociones en memoria incrementando el SP.

Las instrucciones que a causa de su ejecucion afectan a la pila son CALL, INT, RET o IRET. 
- CALL y RET son instrucciones que sirven para invocar y dar el retorno a un procedimiento o subrutina.
- INT e IRET cumplen la misma función cuando se invoca a una subrutina de interrupcion. 

## Interrupciones 
Las interrupciones y excepciones son acontecimientos que provocan un desvio en el flujo de la CPU. 
Las **interrupciones** son acontecimientos externos que activan una patita del microprocesador que desvian el flujo.
Las **excepciones** son internas y se producen como consecuencia de una anomalia dentro de la CPU durante la ejecucion de un programa. 