```console
EJERCICIO 1) 
a) 
	Se puede notar que el tiempo de ejecucion de ambos programas 
	varia entre los 4-5 segundos. No me parece posible predecir el
	valor exacto del tiempo de ejecucion , pero si el rango en el que
	se va a encontrar.
	
b) 
	Mis tiempos de ejecucion          Tiempos de companiero
	                    ---conhilos.py---
	1- 4.05864                              1-4.03202
	2- 4.03445                              2-4.04277
	3- 4.06325                              3-4.06753
	4- 4.11431                              4-4.03352
	5- 4.08229                              5-4.03515
	promedio: 4.07059                       promedio: 4.04220
	
	                    ---sinhilos.py---
	1- 5.28343                              1- 5.44858
	2- 5.31339                              2- 5.44056
	3- 5.27064                              3- 5.46197
	4- 5.35220                              4- 5.43627
	5- 5.25448                              5- 5.44372
	promedio: 5.29483                       promedio: 5.44622
	
	Los tiempos no son identicos, pero son parecidos. Si comparamos 
	nuestros tiempos, podemos ver que los tiempos de ejecucion de mi 
	companiero son mas rapidos en la ejecucion del codigo con hilos
	mientras que el codigo sin hilos se ejecuta mas rapido en mi caso.  
	
c) 
	suma_resta tiempos de ejecucion con comentarios activados:
	1 - 0.02124
	2 - 0.02335
	3 - 0.02437
	4 - 0.02487
	5 - 0.02290
	6 - 0.02304
	7 - 0.02800
	8 - 0.02205
	9 - 0.02872
	10 - 0.02564
	Promedio:  0.02442

	suma_resta tiempos de ejecucion con comentarios desactivados:
	1 - 7.67227
	2 - 8.22251
	3 - 6.79561
	4 - 7.70953
	5 - 7.82679
	6 - 5.87925
	7 - 7.36159
	8 - 7.81554
	9 - 7.76129
	10 - 7.32242
	Promedio: 7.43668
	
	El codigo con los comentarios desactivados tuvo un incremento de
	mas del 30,000% en el tiempo de ejecucion y ademas el resultado 
	paso de ser 0 a ser otro numero. Esto sucede porque al agregar un 
	for loop con 1000 iteraciones en ambas funciones, se sobrecarga 
	el procesador causando que el planificador de tareas cometa muchos 
	mas errores a la hora de dividir equitativamente la suma y la resta. 
	Por eso el acumulador pasa de ser 0 casi siempre a ser cualquier otro 
	numero mucho mas grande. Ejecutando este codigo siempre hay una
	posibilidad de mostrar al acumulador cuando no es 0, al agregar el for 
	loop, se incrementa la posibilidad de que un hilo se interponga ante 
	otro por la sobrecarga del CPU y por eso se muestra un numero que no 
	es 0 con mucha mas frecuencia.  

EJERCICIO 2)
a)
	Codigo race condition solucionado
	
	```console c
#include <pthread.h>
#include <stdio.h>
#include <stdlib.h>
#define NUMBER_OF_THREADS 2
#define CANTIDAD_INICIAL_HAMBURGUESAS 20
int cantidad_restante_hamburguesas = CANTIDAD_INICIAL_HAMBURGUESAS;
int turno = 0;

void *comer_hamburguesa(void *tid)
{
	while (1 == 1)
	{   //printf("\nTID: %d\n", tid); --> Probando el programa
		while(turno!=(int)tid);
		{
        // INICIO DE LA ZONA CRÍTICA
			if (cantidad_restante_hamburguesas > 0)
			{
				printf("Hola! soy el hilo(comensal) %d , me voy a comer una hamburguesa ! ya que todavia quedan %d \n", (int) tid, cantidad_restante_hamburguesas);
				cantidad_restante_hamburguesas--; // me como una hamburguesa
				//printf("Turno = %d + 1 // %d", turno, NUMBER_OF_THREADS); --> Probando el programa
				turno = (turno + 1)% NUMBER_OF_THREADS;
				//printf("\nTURNO: %d\n", turno); --> Probando el programa
			}
			else
			{
				printf("SE TERMINARON LAS HAMBURGUESAS :( \n");

				pthread_exit(NULL); // forzar terminacion del hilo
			}
		}
	// SALIDA DE LA ZONA CRÍTICA

	}
}

int main(int argc, char *argv[])
{
	pthread_t threads[NUMBER_OF_THREADS];
	int status, i, ret;
	for (int i = 0; i < NUMBER_OF_THREADS; i++)
	{
		printf("Hola!, soy el hilo principal. Estoy creando el hilo %d \n", i);
		status = pthread_create(&threads[i], NULL, comer_hamburguesa, (void *)i);
		if (status != 0)
		{
			printf("Algo salio mal, al crear el hilo recibi el codigo de error %d \n", status);
			exit(-1);
		}
	}

	for (i = 0; i < NUMBER_OF_THREADS; i++)
	{
		void *retval;
		ret = pthread_join(threads[i], &retval); // espero por la terminacion de los hilos que cree
	}
	pthread_exit(NULL); // como los hilos que cree ya terminaron de ejecutarse, termino yo tambien.
}


```
```
