## Floating point exception

- ¿Qué función requiere agregar `-DTRAPFPE`? ¿Cómo pueden hacer que el
programa *linkee* adecuadamente?
- Para cada uno de los ejecutables, ¿qué hace agregar la opción `-DTRAPFPE` al compilar? ¿En qué se diferencian 
los mensajes de salida con y sin esa opción?

Si agregamos -DTRAPFPE, el programa incluye la función set_fpe_x87_sse_(), declarada el el archivo fpe_x87_sse.h.
Entonces, para poder compilar con esta opción necesitamos linkear el programa con esa funcion. Osea, tenemos que compilar de la sig manera:
gcc test_fpe1.c ./fpe_x87_sse/fpe_x87_sse.c -DTRAPFPE -lm -o test_fpe1.e

Incluir esta opción hace que en el momento en que se genere una excepción de punto flotante el programa no siga corriendo y no se arrastre ese error.

## Segmentation Fault

#Obtener los ejecutables `small.x` y `big.x`.
#Identifiquen los errores que devuelven (¡si devuelven alguno!) los ejecutables.

Compilamos usando -g, con lo que el código que se ejecuta y el fuente son 1 a 1, sin ningún tipo de optimización.

 *     1) gcc source.c -o small.x -D__SMALL -O0 -g
 *     2) gcc source.c -o big.x -O0 -g 

small.x corre sin ningún problema.
big.x devuelve un Segmentation Fault, la idea es identificar cuál es el problema.

Al correr sin el D__SMALL genera una matriz mucho más grande y de alguna manera tiene problemas para ubicarla en la memoria.

##Ahora ejecuten `ulimit -s unlimited` en la terminal y vuelvan a correrlo. Luego
##responder las siguientes preguntas:
##- ¿Devuelven el mismo error que antes?

Cuando ejecutamos `ulimit -s unlimited` en la terminal el programa big.x corre, aunque tarda muchísimo tiempo.

Mi suposición es que ya sea el sistema operativo ó el mismo programa limita la cantidad de memoria que puede ocuparse, y al ejecutar esa instrucción estamos eliminando esa reestricción.

Mirando lo que arroja `ulimit -a` vemos que se modifica el stack size de 8192kb a "unlimited", permitiendo estructuras de datos de mayor tamaño.

# La "solución" anterior, ¿es una solución en el sentido de debugging?

Creo que no, sólo le damos la posibilidad de manejar estructuras de datos más grandes, imagino que si en algún momento le pedimos que trabaje con matrices mucho más grandes no va a dar la memoria total de la máquina para manejarla y va a volver a explotar, no resolvimos el problema.

## Valgrind
#En la carpeta `valgrind/` hay ejemplos en C y FORTRAN que se pueden ejecutar
#con valgrind. Describan el error y por qué sucede

Ni la más pálida idea cómo funciona el valgrind.

## Funny

En la carpeta `funny/` hay un código de C. Describan las diferencias de los ejecutables
al compilar con y sin el flag `-DDEBUG`. ¿De dónde vienen esas diferencias?

gcc test_oob2.c -o test_oob2.x
./test_oob2.x 
Segmentation fault (core dumped)

gcc test_oob2.c -o test_oob2_debug.x -DDEBUG
./test_oob2_debug.x 
I'm HERE !!!! 
Segmentation fault (core dumped)

Mirando el código no veo demasiadas diferencias, lo único que parece hacer al compilar con -DDEBUG es definir una string y escribirla en la pantalla.


