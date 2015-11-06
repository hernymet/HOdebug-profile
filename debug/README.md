# Debug

Aquí hay tres carpetas, cada una con sus ejercicios. Las respuestas a los ejercicios 
tienen que estar en esta carpeta, bajo el nombre `respuestas.md`

## Floating point exception

En la carpeta `fpe/` hay tres códigos de C, independientes, para compilar. 
Cada uno de estos códigos genera un ejecutable. Hay además una carpeta que
define la función `set_fpe_x87_sse_`. Una vez compilados los tres ejecutables
sin la opción `-DTRAPFPE`, responder las siguientes preguntas:

- ¿Qué función requiere agregar `-DTRAPFPE`? ¿Cómo pueden hacer que el
programa *linkee* adecuadamente?
- Para cada uno de los ejecutables, ¿qué hace agregar la opción `-DTRAPFPE` al compilar? ¿En qué se diferencian 
los mensajes de salida con y sin esa opción?


## Segmentation Fault

En la carpeta `sigsegv/` hay códigos de C y de FORTRAN. Elijan alguno
y compilen y corren el programa de acuerdo a los comentarios en el código,
para obtener los ejecutables `small.x` y `big.x`.
Identifiquen los errores que devuelven (¡si devuelven alguno!) los ejecutables.
Ahora ejecuten `ulimit -s unlimited` en la terminal y vuelvan a correrlo. Luego
responder las siguientes preguntas:

- ¿Devuelven el mismo error que antes?
- Averigüen qué hicieron al ejecutar la sentencia `ulimit -s unlimited`. Algunas pistas
son: abran otra terminal distinta y fíjense si vuelve al mismo error, fíjense la diferencia
entre `ulimit -a` antes y después de ejecutar `ulimit -s unlimited`, googleen, etcétera.
- La "solución" anterior, ¿es una solución en el sentido de debugging?

## Valgrind

En la carpeta `valgrind/` hay ejemplos en C y FORTRAN que se pueden ejecutar
con valgrind. Describan el error y por qué sucede

## Funny

En la carpeta `funny/` hay un código de C. Describan las diferencias de los ejecutables
al compilar con y sin el flag `-DDEBUG`. ¿De dónde vienen esas diferencias?








