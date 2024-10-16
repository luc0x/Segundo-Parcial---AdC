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
