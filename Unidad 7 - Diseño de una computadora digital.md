# Unidad 7 - Diseño de una Computadora Digital
### Modulo
Compuesto por una configuracion determinada de compuertas, un modulo es el encargado de **realizar una o varias operaciones** sobre datos codificados en binarios que se almacenan en **registros** asociados al modulo mientras se realiza la operacion.

Si dentro de un modulo, una operacion se aplica a un **registro**, esta se denomina **microoperacion** y se activa en **un instante de tiempo sincronizado por los pulsos de del reloj**.

## Registros en IA-32
![](https://lh5.googleusercontent.com/proxy/tuN0TC6L6Xju4b7_hiK3_Xc9a4trr0s4vZRgZR0XRGKzyYcBEHIGkAqr5Ni_OwNCG6tAjOpYw2F2eBYZwkVVyXqawnIsQsBQ-5fbTaD3ieprSYCaeh8GmdNGuaDH7QQZ4OIhASVEO8c_fndaVRfDChe7D90m_qxUva5Rpo2KCA)
### Registros de porposito general
Los cuatro registros de calculo diseñados para ser utilizados para operaciones aritmeticas y logicas son:
1. EAX - **Accumulator**
2. EBX - **Base**
3. ECX - **Counter**
4. EDX - **DATA**

AGREGADO:
La letra E delante del registro vienen de **"Extended"** y tiene con que estas accediendo a los 32 bits del registro. 
En el caso de que quieras acceder a 16 bits del registro se usa como siempre (AX, BX, CX, DX) y si se quiere acceder a 8bits se puede utilizar tanto AH BH CH DH para acceder a los 8 bits mas significativos como AL BL CL DL para los bits menos significativos. 
### Registros punteros
Los registros punteros tienen un tamaño por defecto de 32 bits con la posibilidad de usarlos como 16 bits para mantener la compatibilidad. Estos son:
1. IP [**Instruction Pointer**]: Es el registo encargado de apuntar a la proxima instruccion
2. SP [**Stack Pointer**]: Es un registro encargado de apuntar al final de la pila.
3. BP [**Base Pointer**]: Es el registro encargado de 