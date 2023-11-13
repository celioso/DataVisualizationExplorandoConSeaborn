# Data Visualization Explorando con Seaborn

###  Preparando el ambiente
Bienvenidos y bienvenidas al curso Data Visualization: Explorando con Seaborn

Yo soy el instructor Mauricio Loaiza y en este curso haremos análisis de datos utilizando la biblioteca Pandas y análisis visual y de gráficos con la biblioteca Seaborn, que Python nos ofrece.

En este [link](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/tree/aula1 "link") puedes encontrar la base con la que estaremos trabajando a lo largo de este curso. O si deseas puedes descargar el archivo zip haciendo [click aquí](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/archive/refs/heads/aula1.zip "click aquí").

### Ambiente de Análisis

En este curso usaremos la herramienta Colaboratory o Google Colab que Google nos ofrece de forma gratuita. Esta herramienta es un Jupyter notebook que no requiere ninguna configuración.

### Colaboratory

Para usar este ambiente es necesario tener una cuenta en google, dado que los notebooks que son creados en Colaboratory quedarán guardados en Google Drive.

En este link puedes crear una cuenta de Google, caso no la tengas: [Crea una cuenta de Google](https://accounts.google.com/signup/v2/webcreateaccount?flowName=GlifWebSignIn&flowEntry=SignUp "Crea una cuenta de Google").

### Informaciones adicionales sobre Colaboratory

- El código de tu notebook es ejecutado en una máquina virtual dedicada a tu cuenta. Las máquinas virtuales son recicladas por un determinado tiempo.
- Cada vez que abramos nuestro notebook, será necesario hacer upload del archivo que queramos analizar.

### ¿Puedo usar un ambiente diferente a Google Colaboratory?

Si, no habría ningún problema. Una opción sería [Anaconda](https://www.anaconda.com/download "Anaconda").

Los espero en la siguiente clase.

### Haga lo que hicimos en aula

Como informamos anteriormente, en este curso trabajaremos con las bibliotecas de Pandas y Seaborn.

Comenzamos importando la biblioteca Pandas para poder traer la base que usaremos en el curso

```python
import pandas as pd
```
Después usamos pandas para leer la base y guardar como un DataFrame con el nombre de datos.

Así como mencionamos en el video 1.2, debemos subir la base de datos a Google Colaboratory caso estés usando esta herramienta:

```python
datos = pd.read_csv(‘credit_card.csv’)
```
Podemos hacer una visualización inicial de nuestra base de datos usando la función `head()` e `info()`. La primera nos permite ver, por defecto, el nombre de las columnas y las primeras 5 líneas de cada una de ellas:
```python
datos.head()
```

La segunda nos muestra las características de las variables en nuestra base de datos, la cantidad de líneas en cada una de ellas y el tipo de variable, si es un número entero o decimal, o si es una variable de texto.
```python
datos.info()
```
Por motivos didácticos decidimos traducir al español el nombre de las columnas y los contenidos dentro de ellas dado que la base originalmente está en inglés.

Primero seleccionamos las columnas,
```python
datos.columns
```
Enseguida creamos un Diccionario con el nombre de las columnas y el nombre que queremos para ellas:
```python
dic_columnas = {
    'LIMIT_BAL' : 'limite', 
    'CHECKING_ACCOUNT' : 'cuenta_corriente', 
    'EDUCATION' : 'escolaridad', 
    'MARRIAGE' : 'estado_civil', 
    'AGE' : 'edad',
    'BILL_AMT' : 'valor_factura', 
    'PAY_AMT' : 'valor_pago', 
    'DEFAULT' : 'moroso'
}
```
Después de crear nuestro Diccionario, usamos la función rename y en este momento creamos un nuevo DataFrame (tarjetas) ya con el nombre de nuestras columnas traducidas.
```python
tarjetas = datos.rename(columns = dic_columnas)
```
Ya tenemos el nombre de nuestras columnas en español, ahora debemos traducir los campos de nuestras columnas de texto en la base.

**Variable cuenta corriente**

Comenzaremos con la variable `cuenta_corriente`. Primero identificamos los campos que tenemos en esta columna con la función `unique()`.

```python
tarjetas.cuenta_corriente.unique()
```
Después crearemos un nuevo diccionario con los campos identificados y con el nombre que queramos darle a estos campos.
```python
dic_cuenta = {
    'Yes' : 'Si', 
    'No' : 'No'
}
```
Y finalmente usamos el diccionario creado para actualizar los campos en la base de datos.

En el lado izquierdo de la función está el nombre de la base datos y la columna que queremos alterar. En la parte derecha seleccionamos de nuevo la base de datos, la columna que vamos a ajustar y la función map() con el diccionario como parámetro.

```python
tarjetas.cuenta_corriente = tarjetas.cuenta_corriente.map(dic_cuenta)
```
Haremos un proceso similar para las demás variables que están en formato texto.

**Variable escolaridad**
```python
tarjetas.escolaridad.unique()
dic_escolaridad = {
    '2.University' : '2.Universidad', 
    '3.Graduate School' : '3.Pos-graduación', 
    '1.High School' : '1.Colegio'
}
tarjetas.escolaridad = tarjetas.escolaridad.map(dic_escolaridad)
```
**Variable estado civil**
```python
tarjetas.estado_civil.unique()
dic_estado_civil = {
    'Married' : 'Casado/a', 
    'Single' : 'Soltero/a'
}
tarjetas.estado_civil = tarjetas.estado_civil.map(dic_estado_civil)
```

### Lo que aprendimos

Lo que aprendimos en esta aula:

- Hacer upload de archivo csv para Google Colab. Importamos pandas e importamos la base de datos con la que vamos a trabajar en el curso: credit_card.csv.
- Conocimos nuestra base de datos y las variables que vamos a analizar en clase.
- Por cuestiones didácticas decidimos hacer la traducción al español de las variables categóricas en la base que se encontraban en inglés.
- Guardamos nuestra base de datos con el nombre de tarjetas.

### Proyecto del aula anterior

¿Comenzando en esta etapa? Aquí puedes descargar los archivos del proyecto que hemos avanzado hasta el aula anterior.

[Descargue los archivos en Github](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/tree/aula1 "Descargue los archivos en Github") o haga clic [aquí](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/archive/aula1.zip "aquí") para descargarlos directamente.

### Haga lo que hicimos en aula

Para esta aula y para las siguientes aulas usaremos Seaborn, una biblioteca para análisis visual de datos. Para hacer la instalación puedes usar pip, así como está descrito abajo.

Si estás usando Google Colaboratory, la biblioteca ya está instalada.

```python
!pip install seaborn
```
Usaremos la versión 0.11

Para importar Seaborn en nuestro notebook lo hacemos de la siguiente forma:
```python
import seaborn as sns
```
Usamos sns por convención.

Vamos a comenzar mostrando un ejemplo de las imágenes que podemos crear con Seaborn usando la función `displot`.

Esta función nos permite ver la función de una variable:
```python
sns.displot(data=tarjetas, x='limite', hue='escolaridad')
```
- data: es nuestra base de datos
- x: es la variable numérica que vamos a analizar.

**Creación de variable**

Ahora crearemos una nueva variable en nuestra base de datos, esto para profundizar en el entendimiento de nuestra variables y poder crear relaciones entre ellas. Crearemos el Índice de Uso (IU) que es el porcentaje que usamos del total de límite disponible que tenemos.
```python
tarjetas['iu'] = tarjetas['valor_factura'] / tarjetas['limite']
```
Y generamos nuevamente un gráfico de distribución para saber cómo se comporta nuestra variable con los clientes que tenemos en la base de datos:
```python
sns.displot(data=tarjetas, x='iu')
```
**Algunas características de Seaborn**

Seaborn es una biblioteca que usa la biblioteca Matplotlib para realizar todos sus procesos. Dado este hecho, algunas características de Matplotlib están disponibles para nosotros en Seaborn, por ejemplo, podemos usar las opciones de colores que Matplotlib nos ofrece para personalizar nuestros gráficos de la forma que queramos.

En este [link](https://matplotlib.org/3.1.0/tutorials/colors/colormaps.html "link") podemos conocer todas las opciones de colores que tenemos disponibles.

Para hacer uso de esta usamos el parámetro `palette` en nuestras funciones de Seaborn.

Como ejemplo:
```python
sns.displot(data=tarjetas, x='limite', hue='escolaridad', palette='inferno_r');
```
Seaborn también nos permite dar algunos estilo a nuestros gráficos, para hacer uso de esto, podemos usar la función `set_style()`

Solo debemos ejecutarla una vez y todos los gráficos que generemos después de la ejecución ya estarán parametrizados, las opciones que tenemos son: `(darkgrid, whitegrid, dark, white, ticks)`, ejemplo:
```python
sns.set_style(‘darkgrid’)
```
### Lo que aprendimos

Lo que aprendimos en esta aula:

- Importamos Seaborn para analizar de forma gráfica las variables que tenemos en nuestra base de datos.
- Construimos una nueva variable numérica en nuestra base de datos.
- Creamos un histograma para analizar variables en nuestra base de datos.
- Descubrimos los estilos y colores que Seaborn nos ofrece.

### Proyecto del aula anterior

¿Comenzando en esta etapa? Aquí puedes descargar los archivos del proyecto que hemos avanzado hasta el aula anterior.

[Descargue los archivos en Github](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/tree/aula2 "Descargue los archivos en Github") o haga clic [aquí](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/archive/aula2.zip "aquí") para descargarlos directamente.

### Haga lo que hicimos en aula

En esta aula conocemos algunos gráficos que nos permiten analizar fácilmente variables categóricas o de texto.

**Countplot**

Este gráfico nos permite contar el número de vezes que una opción se repite en una variable, por ejemplo, la variable Cuenta corriente tiene las opciones `Si` y `No`, con countplot podemos contar el numero de vezes que cada una está en la base.

```python
sns.countplot(x='cuenta_corriente', data= tarjetas)
```
No sólo eso, con el parámetro `hue` de esta función podemos traer otra variable para nuestro gráfico y analizarla al lado de nuestra variable `x`. Podemos aprovechar para usar el parámetro `palette` y personalizar un poco nuestro gráfico.
```python
sns.countplot(x='cuenta_corriente', data= tarjetas, hue='moroso', palette='coolwarm')
```
**Catplot**

Este gráfico nos permite comparar una variable categórica (eje x) y una variable numérica (eje y). Podemos ver cómo está distribuida nuestra variable categórica en relación con nuestra variable numérica:
```python
sns.catplot(x='estado_civil', y='limite', data=tarjetas)
```
De la misma forma podemos usar el parámetro `hue`, para traer otra variable a nuestro gráfico, también usamos el parámetro dodge para que se muestran columnas diferentes para esta variable y no se agrupen solamente en una columna.
```python
sns.catplot(x='estado_civil', y='limite', data=tarjetas, hue='moroso', dodge=True)
```
**Swarmplot**

Es un gráfico bastante parecido al `catplot` solo que en este gráfico los puntos de nuestra variable no se sobreponen. Por este detalle, cuando la base de datos es muy grande es posible que algunos datos se pierdan.
```python
sns.swarmplot(x='escolaridad', y='iu', data=tarjetas)
```
**Boxplot**

En este gráfico analizamos también una variable categórica y una variable numérica, nos permite observar más información de nuestra variable analizada. Aquí podemos usar también algunos parámetros como `hue` o `palette`.

```python
sns.boxplot(x='escolaridad', y='iu', data=tarjetas, hue='moroso', palette='bone')
```
Comencemos viendo el rectángulo, la línea inferior es el percentil 25%, la línea superior es el percentil 75% y la línea que cruza el rectángulo es el percentil 50% o la mediana.

Hay dos líneas perpendiculares que van más allá de las medidas del rectángulo, el punto inferior de la línea que va hacia abajo es el punto mínimo en nuestra variable, y el punto máximo de la línea que va hacia arriba es el punto máximo.

Si hay puntos más allá de estos dos líneas, estos son considerados outliers.

**Violinplot**

Este gráfico es muy parecido al boxplot, sólo que en este caso podemos ver la distribución de forma vertical en cada parámetro de nuestro gráfico.
```python
sns.violinplot(x='escolaridad', y='iu', data=tarjetas, hue='moroso')
```
**Creación de variable categórica a partir de una variable numérica**

Vamos a analizar ahora una variable numérica, la edad, como podemos deducir, en esta variable tenemos muchos valores, desde 18 hasta 75 años (edad máxima en nuestra base de datos), para facilitar el análisis vamos a agruparlas en grupos. Haremos esto usando la función `cut` de pandas.

Podemos saber las edades que tenemos en nuestra base de datos usando la siguiente fórmula:
```python
tarjetas.edad.unique()
```
Crearemos 4 rangos usando el siguiente código:
```python
bins = [18, 30, 40, 50, 100]
nombres = ['18-30', '30-40', '40-50', '50+']
tarjetas['rango_edad'] = pd.cut(tarjetas['edad'], bins, labels=nombres)
```
Los valores en la lista bins se usan como los límites mínimos y máximos de nuestros rangos. Lo que tenemos en nuestra lista `nombres` son los nombres de nuestros rangos, y en la tercera línea usamos la función `cut` para crear nuestra variable en la base de datos con el nombre `rango_edad`.

Podemos analizarla inicialmente con un `boxplot` para ver su distribución inicial:
```python
sns.boxplot(x='rango_edad', y='limite', data= tarjetas);
```

**Lo que aprendimos**

Lo que aprendimos en esta aula:

- Aprendimos a crear diferentes gráficos que nos ayudan a analizar variables categóricas: countplot, catplot, swarmplot.
- Aprendimos a usar el parámetro hue, que nos sirve para fraccionar una variable en nuestro gráfico.
- Introducimos los gráficos boxplot y violinplot.
- Creamos y analizamos con boxplot la variable categórica rango_edad.

### Proyecto del aula anterior

¿Comenzando en esta etapa? Aquí puedes descargar los archivos del proyecto que hemos avanzado hasta el aula anterior.

[Descargue los archivos en Github](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/tree/aula3 "Descargue los archivos en Github") o haga clic [aquí](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/archive/aula3.zip "aquí") para descargarlos directamente.

### Haga lo que hicimos en aula

**Gráfico de distribución**

En esta aula haremos el análisis de variables numéricas, comenzaremos profundizando en el gráfico de distribución del que ya hablamos anteriormente.

En esta función también podemos usar algunos parámetros para hacer comparaciones de variables.

```python
sns.displot(data=tarjetas, x='limite', col='escolaridad', kind='kde');
```
Con el parámetro `col`, la función nos abre un gráfico para cada campo dentro de la variable que estamos analizando.

Con el parámetro `hue`, podemos ver várias distribuciones dentro de un mismo gráfico, cada campo de la variable tendrá una distribución diferente:
```python
sns.displot(data=tarjetas, x='limite', kind='kde', hue='rango_edad');
```
**Gráfico de dispersión y línea de regresión**

El gráfico de dispersión nos muestra cómo se relacionan dos variables numéricas y si existe alguna tendencia o correlación entre ellas, la podemos usar de la siguiente forma:
```python
sns.scatterplot(x='iu', y='valor_factura', data=tarjetas);
```
En esta función podemos usar el parámetro hue, lo que nos permitirá abrir varias dispersiones en el gráfico, una para cada campo de nuestra variable.

```python
sns.scatterplot(x='iu', y='valor_factura', data=tarjetas, hue='cuenta_corriente');
```
La línea de dispersión la podemos ver usando la función `lmplot` (linear model plot), este gráfico nos mostrará también un gráfico de dispersión y la línea de regresión que mejor se ajuste a la relación entre las dos variables:
```python
sns.lmplot(x='iu', y='valor_factura', data=tarjetas);
```
**Test de hipótesis**

Ahora realizaremos un test de hipótesis con la variable moroso, para conocer si estos dos grupos (moroso y no moroso) son estadísticamente diferentes o no.

Comenzamos importando la biblioteca scipy de python, dado que la usaremos para calcular más adelante el p-value.
```python
from scipy.stats import ranksums
```
Nuestras hipótesis nula y alternativa serán respectivamente:

**Hipótesis nula**: La distribución de los grupos moroso y no moroso es la misma

**Hipótesis alternativa**: La distribución de los grupos moroso y no moroso no es la misma

Separamos los grupos moroso y no moroso usando el valor de la factura como base:

```python
moroso = tarjetas.query("moroso == 1").valor_factura
no_moroso = tarjetas.query("moroso == 0").valor_factura
```
Usamos la función ranksums de scipy para calcular el p-value:
```python
ranksums(moroso, no_moroso)
```

### Lo que aprendimos

Lo que aprendimos en esta aula:

- Hicimos un análisis más profundo de los gráficos de distribución (histograma) usando displot.
- Creamos gráficos diferentes, categorizando nuestra información con el parámetro col.
- Hicimos una introducción al gráfico de dispersión (scatterplot) y al gráfico de modelo linear (lmplot).
- Realizamos un test de hipótesis, para intentar determinar si la diferencia entre los grupos morosos y no morosos es estadísticamente significativa.

### Proyecto del aula anterior

¿Comenzando en esta etapa? Aquí puedes descargar los archivos del proyecto que hemos avanzado hasta el aula anterior.

[Descargue los archivos en Github](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/tree/aula4 "Descargue los archivos en Github") o haga clic [aquí](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/archive/aula4.zip "aquí") para descargarlos directamente.

### Haga lo que hicimos en aula 

**Jointplot**

El `jointplot` nos permite analizar al mismo tiempo la distribución de dos variables de forma individual y como se relacionan estas variables entres ellas. En este gráfico también podemos usar el parámetro `hue` para analizar nuestros gráficos a partir de otra variable.

```python
sns.jointplot(x='edad', y='limite', data=tarjetas, kind='kde', hue='moroso')
```
Podemos definir el tipo de gráfico que queremos mostrar con el parámetro `kind`, las opciones que éste parámetro nos permite son:
```python
(“scatter”, “kde”, “hist”, “hex”, “reg”, “resid” )
```
**Pairplot**

El `pairplot` nos permite visualizar con una línea de código cómo se relacionan todas las variables numéricas en nuestra base de datos, cuando la misma variable se cruza en la fila y la columna tendremos un gráfico de distribución, cuando se cruza una variable con las demás tendremos un gráfico de dispersión,

En este gráfico también podemos usar el parámetro `hue` para incluir otra variable categórica en el análisis de los gráficos o el parámetro `palette` para darle una personalización a nuestro gráfico.
```python
sns.pairplot(data=tarjetas, hue='escolaridad', palette='cividis')
```

### Proyecto Final

Aquí puedes descargar los archivos del proyecto completo.

[Descargue los archivos en Github](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/tree/aula5 "Descargue los archivos en Github") o haga clic [aquí](https://github.com/alura-es-cursos/1779-Data-Visualization-Explorando-con-Seaborn/archive/aula5.zip "aquí") para descargarlos directamente.

### Lo que aprendimos

Lo que aprendimos en esta aula:

- Introducimos el gráfico jointplot con sus opciones: scatter, kde, hex. Esto para analizar la variable de edad y limite.
- Hicimos un análisis descriptivo de las variables en nuestra base de datos.
- Usamos el gráfico pairplot para hacer un análisis conjunto de todas nuestras variables numéricas en la base de datos.