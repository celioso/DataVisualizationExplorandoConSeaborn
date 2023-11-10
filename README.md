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