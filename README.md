# Ayudantia 4: Práctica de Redes


En la clase de ayudantía de hoy pondremos en práctica lo revisado anteriormente. 

Dividanse en dos grupos y daremos 1 hora y 20 min para cada ejercicio.

Al final de la clase, entregue un reporte con sus respuestas. Este puede ser un HTML.

# Ejercicio 1: Redes de cooperación en cursos

Vamos a trabajar con datos del proyecto "Juecoo" realizado por investigadores de nuestra universidad. Se le entrega un subconjunto anonimizado con una selección de datosdatos disponible en la carpeta. El grupo 1 trabaje con el curso 1 y el grupo 2 con el curso 2.

1. Identifique las variables disponibles con las que cuente y realice una breve estadística descriptiva.

2. Filtre sus datos para el curso con el cual le toca trabajar.

3. Creemos una red en base a los datos, en los cuales definiremos un link entre dos individuos si hay al menos un envio de 10 entre ellos. No importa quien realice el envio.  Esta es una red no dirigida sin pesos. 

4. Realice una visualización de la red.

5. Calcule la centralidad de grado y reagile un histograma de esta. ¿QUé información puede interpretar de este resultado.

6. Ahora creemos una segunda red para el curso, pero esta vez definiremos un link entre dos individuos hay un envio de 10 entre ellos, pero preservaremos la información de quien realiza el envio. Es decir, debe crear una edgelist con dos elementos: from y to. Esta es una red no dirigida sin pesos. 

7. Calcule la centralidad de grado, in degree y outdegree y realice un histograma de estas. ¿Qué información puede interpretar de este resultado.

8. Agreguege a ambas visualizaciones el grado como atributo del nodo y úselo para su tamaño.

9. Agregue a ambas visualizaciones el género como un atributo del nodo y coloree los nodos de acuerdo a este. 

(Propuesto: Finalmente, cree una lista de adjaciencia con pesos para su curso. Esta lista debe tener columnas elementos: from, to, weight (que corresponde al link) y replique la visualización, esta vez agregando un atributo al link que indique el grosor como el peso)

# Ejercicio 2: Carreras más matriculadas por región.

Para este segundo ejercicio, trabajaremos los datos de postulación a carreras universitarias en chile. Para esto contamos con la sigiguiente [carpeta de datos](https://www.dropbox.com/sh/uw9u1wlwi189lbw/AAD9rRWQsBLskP3hexaOk08Ba?dl=0)

Cuando queremos hacer rankings, en general no basta con solo contar la frecuencia de eventos. Tenemos que considerar efectos de tamaños. Por ejemplo, para hacer comparables todas las carreras y todas las regiones, necesitamos considerar la cantidad total de postulantes de cada región y la cantidad de postulaciones a cada carrera. Una medida que controla por estos dos factores es el Balassa Index o RCA.

Por lo general, $M_{cp}$ se define como $M_{cp} = 1$ cuando la cantidad de postulaciones a una carrera en una comuna es mayor que lo esperado para una comuna del mismo tamaño y una carrera con la misma cantidad de postulciones.

$$ M_{cp} = 1 \quad \text{if} \quad R_{cp} \geq 1$$

Donde
$$ R_{cp}= \fraq{X_{cp}}{X_c X_o / X}$$

- $X_{cp}$ es la matriz que asocia comunas y carreras y cada entrada corresponde al número de postulaciones en una comuna c de una carrera p. 
- $X_{p} = \sum_p X_{cp}$ es el vector que contiene el número de postulaciones en todas las carreras para cada comuna c.
- $X_{c} = \sum_{p} X_{cp}$ es el vector que contiene el número de postulaciones en todas las comunas para cada carrera p. 
- $X = \sum_{cp} X_{cp}$ es el número total de postulaciones. 

Por tanto, el denominador de la ecuación $R_{cp}$ corresponde a las postulaciones esperadas de la comuna c para la carrera p. En otras palabras, el denominador es igual a la cantidad de postulaciones de una comuna ($X_c = \sum_p X_{cp}$) multiplicado por la cantidad de postulaciones totales a esa carrera (X = [eXçp) dividido por el número total de postulaciones utilizadas en todo el país (L Xp).


1) Para cada región, construya el ranking de las top-10 carreras más postuladas en primera opción. (Ordene las columnas usando el Balassa index no-discreto; balassa_index(incidence_matrix_1st,discrete=F))

2) Construya el ranking top-10 para las siguientes comunas: Santiago, Las Condes, Vitacura, Providencia, Puente Alto, Maipú, Concepción, Valparaíso, Viña del Mar, La Serena, Antofagasta, Iquique, Arica, Rancagua, Talca, Linares, Los Ángeles, Chillán, Temuco, Osorno, Puerto Montt, Castro, Chiloé, Aysén, Punta Arenas.

3) Grafique la red de carreras usando balassa_index(incidence_matrix_1st, discrete = T) y avg_links = 8.

4) Repita el punto 2 con una red a nivel a nivel región y comuna (ojo con los valores nan de la matriz de proximidad).




