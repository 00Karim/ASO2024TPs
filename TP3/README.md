1) 
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
	suma_resta tiempos de ejecucion con comentarios:
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

	suma_resta tiempos de ejecucion sin comentarios
	1 - 0.02398
	2 - 0.01890
	3 - 0.02261
	4 - 0.01868
	5 - 0.02357
	6 - 0.02002
	7 - 0.02404
	8 - 0.01864
	9 - 0.02518
	10 - 0.02203
	Promedio: 0.02240
	
	El tiempo de ejecucion sin comentarios tuvo una disminucion del
	8.3% de tiempo de ejecucion. Ademas, paso de estar siempre por 
	encima de 0.021 a poder estar por debajo en 4/10 casos.
	Me parecio que no tenia sentido esto, asi que investigue
	y al parecer los comentarios no afectan el tiempo de ejecucion
	de un codigo python porque el interprete de python directamente
	ignora los comentarios durante la ejecucion. 
	Parece ser que simplemente no use una cantidad de datos 
	significativa para representar la diferencia entonces
	se sesgaron mis resultados.
	Entonces: Que paso? Se ejecuto el codigo normalmente.
		  Por que? Por lo explicado anteriormente. 
