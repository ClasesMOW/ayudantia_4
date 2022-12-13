# Ayudantia 4: Práctica de Redes


En la clase de ayudantía de hoy pondremos en práctica lo revisado anteriormente. 

Dividanse en dos grupos y daremos 1 hora y 20 min para cada ejercicio.

Al final de la clase, entregue un reporte con sus respuestas. Este puede ser un HTML.

# Ejercicio 1: Redes de cooperación en cursos

Vamos a trabajar con datos del proyecto "Juecoo" realizado por investigadores de nuestra universidad. Se le entrega un subconjunto anonimizado con una selección de datosdatos disponible en la carpeta. El grupo 1 trabaje con el curso 1 y el grupo 2 con el curso 2.

1. Identificque las variables disponibles con las que cuente y realice una breve estadística descriptiva.

2. Filtre sus datos para el curso con el cual le toca trabajar.

3. Creemos una red en base a los datos, en los cuales definiremos un link entre dos individuos si hay al menos un envio de 10 entre ellos. No importa quien realice el envio.  Esta es una red no dirigida sin pesos. 

4. Realice una visualización de la red.

5. Calcule la centralidad de grado y reagile un histograma de esta. ¿QUé información puede interpretar de este resultado.

6. Ahora creemos una segunda red para el curso, pero esta vez definiremos un link entre dos individuos hay un envio de 10 entre ellos, pero preservaremos la información de quien realiza el envio. Es decir, debe crear una edgelist con dos elementos: from y to. Esta es una red no dirigida sin pesos. 

7. Calcule la centralidad de grado, in degree y outdegree y realice un histograma de estas. ¿Qué información puede interpretar de este resultado.

8. Agreguege a ambas visualizaciones el grado como atributo del nodo y úselo para su tamaño.

9. Agregue a ambas visualizaciones el género como un atributo del nodo y coloree los nodos de acuerdo a este. 

( Finalmente, cree una lista de adjaciencia con pesos para su curso. Esta lista debe tener columnas elementos: from, to, weight (que corresponde al link) y replique la visualización, esta vez agregando un atributo al link que indique el grosor como el peso)

# Ejercicio 2: Carreras más matriculadas por región.

Para este segundo ejercicio, trabajaremos con la red de carreras. 

Cuando queremos hacer rankings, en general no basta con solo contar la frecuencia de eventos. Tenemos que considerar efectos de tamaños. Por ejemplo, para hacer comparables todas las carreras y todas las regiones, necesitamos considerar la cantidad total de postulantes de cada región y la cantidad de postulaciones a cada carrera. Una medida que controla por estos dos factores es el Balassa Index o RCA.

Por lo general, $M_{cp}$ se define como $M_{cp} = 1$ cuando la cantidad de postulaciones a una carrera en una comuna es mayor que lo esperado para una comuna del mismo tamaño y una carrera con la misma cantidad de postulciones.

$$ M_{cp} = 1 \quaq \text{if} \quad R_{cp} \geq 1$$

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



# Ejercicio 3: Matching

Vamos a replicar el estudio [Dynamics of cross-platform attention to retracted papers](https://www.pnas.org/doi/10.1073/pnas.2119086119).

En este trabajo los autores estudian la atención recibida por los papers que han sido retractados. 

Los autores pusieron a disposición de la comunidad un [repositorio en github](https://github.com/haoopeng/retraction_attention) con los datos procesados y los algoritmos usados para obtener los resultados de la investigación. Nosotros contamos con un set de datos alternativos para aproximarnos a su trabajo disponibles en la siguiente [carpeta de dropbox](https://www.dropbox.com/sh/cjfgznuhc3oj3jp/AACNJFqozxyEgrBeX2eBLgI0a?dl=0)


Los autores usan tres fuentes de datos: 

-  Altmetric que se puede acceder por investigadores en https://www.altmetric.com/research-access/ 

-  The Retraction Watch database que está disponible para investigadores del The Center For Scientific Integrity  sujeto a un acuerdo de uso de datos  (detalles en https://retractionwatch.com/retraction-watch-database-user-guide/). 

-  The Microsoft Academic Graph is publicly available at https://www.microsoft.com/en-us/research/project/microsoft-academic-graph/ or https://www.microsoft.com/en-us/research/project/open-academic-graph/. 
  
-  También usan datos de tweets.  Dado resguardo de la privacidad d elos usuarios, Twitter no permite compartir directamente el texto de los tweets. Para cumplir con este requerimiento, los autores proveen una identificación de los tweets como critical/uncritical. (https://developer.twitter.com/en/products/twitter-api/academic-research).


Como vemos, varios de estos datos están sujetos a inscripcion de los investigadores y no pueden ser publicados directamente. Los autores ponen a nuestra disposición su código de trabajo (en una colección de notebooks), pero no los datos raw sino procesados.

Con estos datos procesados, podemos replicar directamente las tablas de resultado del trabajo.  Para poder hacer el match nosotros, necesitaremos más datos de los que ellos nos han compartido.

El ejericio se compone de tres tareas:

1. Replicar el match usando los datos de medicina. Para cada articulo identifique dos clones usando PSM.
2. Estimar los resultados con nuestro match
(3. Replicar los resultados con el match de los autores)
3. Comparar los resultados obtenidos con el de los autores
