# RETO11
## Strings
## 1. Consulte que hacen los siguientes métodos de strings en python: endswith, startswith, isalpha, isalnum, isdigit, isspace, istitle, islower, isupper.
## endswith() método
Este método de string en python verifica que una cadena de texto termine con un determinado sufijo, o varios. Si si termina con el valor especificado devuelve Trure, en caso contrario devuelve False, se escribe de la siguiente manera:
```
cadena.endswith(sufijo, inicio, fin)

```
Donde    
- sufijo es el valor (cadena o tupla de cadenas) que se quiere verificar. Es obligatoro.
- inicio y fin son los que indican en que rango (donde empezar y donde terminar) de la cadena buscar. Es opcional.  
Ejemplo donde se compureba que la cadena termina en en un rango definido
```
nombre = "mi_archivo.txt"

print(nombre.endswith(".txt", 0, 11))  
print(nombre.endswith(".txt", 0, 14))   
print(nombre.endswith(".py", 0, 14))
```
## startswith()
Basicamente hace lo mismo que endswith pero con los valores con los que inicia la cadena.   
La sintaxis es 
```
cadena.startswith(prefijo, inicio, fin)
````
Aquí el prefijo es el valor que queremos verificar  
Ejemplo donde se comprueba que la cadena empiece con Hola
```
mensaje = "Hola mundo"

print(mensaje.startswith("Hola"))     
print(mensaje.startswith("Mundo"))  
print(mensaje.startswith(("Hola", "Hey"))) 
```
## isalpha()
Este metodo verifica que los carácteres de la cadena pertenezcan al alfabeto (A-Z), o que no esté vacía, por lo que Devuelve True si son letras y no está vacía, y False si hay espacios, números, símbolos o está vacía.  
Su sintaxis es
```
cadena.isalpha()
```
Ejemplo donde devuelve False por el espacio.
```
print("Hola Mundo".isalpha())
```
## isalnum()
Verifica  que los carácteres de la cadena pertenezcan al alfabeto (A-Z), que no esté vacía o que sean números, por lo que Devuelve True si son letras, números o no está vacía, y False si hay espacios, símbolos o está vacía.  
Su sintaxis es 
````
cadena.isalnum()
````
Ejemplo
```
print("Hola".isalnum())   
```
## isdigit()
Verifica  que los carácteres de la cadena sean números, este devuelve True solo si son números o no está vacía, y False si hay espacios, símbolos, letras o está vacía.    
Su sintaxis es 
````
cadena.isalnum()
````
Ejemplo
```
print("Hola".isalnum())   
```
## isspace()
Verifica si todos los caracteres de una cadena son espacios en blanco. Por lo que devuelve True si todos los caracteres son espacios (como ' ', \n, \t, etc.) y la cadena no está vacía y 
False si hay letras, números, símbolos o si está vacía.  
Su sintaxis es 
````
cadena.isspace()
````
Ejemplo
```
print("   ".isspace())
```
## istitle()
Verifica que cada palabra comienza con una letra mayúsculay que el resto de cada palabra esté en minúscula. Los números, simbolos o espacios no afectan.  
Su sintaxis es
````
cadena.istitle()
````
Ejemplo
````
print("Hola Mundo 123".istitle())  
````
##  islower()
Verifica si todos los caracteres alfabéticos en una cadena están en minúscula, ignora números y simbolos, si nes una cadena vacía devuelve False  
Su sintaxis es 
```
cadena.islower()
```
Ejemplo
```
print("hola mundo".islower())
```
##  isupper()
Verifica si todos los caracteres alfabéticos en una cadena están en mayuscula, ignora números y simbolos, si nes una cadena vacía devuelve False    
Su sintaxis es 
```
cadena.isupper()
```
Ejemplo
```
print("HOLA MUNDO".isuper())
```
## 2. Procesar el archivo y extraer:

- Cantidad de vocales
- Cantidad de consonantes
- Listado de las 50 palabras que más se repiten  

Utilicé urllib.request para poder manipular el texto en URL. 
```
import urllib.request

url = "https://www.py4e.com/code3/mbox.txt"
nombre_archivo = "archivo.txt"
urllib.request.urlretrieve(url, nombre_archivo)

print("Archivo descargado como", nombre_archivo)
```
Código para contar la cantidad de vocales y consonantes y 50 palabras mas repetidas
```
def contar_vocales_consonantes(texto):
    vocales = "aeiouAEIOU"
    num_vocales = 0
    num_consonantes = 0

    for letra in texto:
        if letra.isalpha():
            if letra in vocales:
                num_vocales += 1
            else:
                num_consonantes += 1

    return num_vocales, num_consonantes

def palabras_mas_frecuentes(texto):
    palabras = texto.split()
    palabras_limpias = []

    for palabra in palabras:
        if palabra.isalpha():  # Solo palabras con letras
            palabras_limpias.append(palabra.lower())

    lista_frecuencias = []

    for palabra in palabras_limpias:
        encontrado = False
        for i in range(len(lista_frecuencias)):
            if lista_frecuencias[i][0] == palabra:
                lista_frecuencias[i][1] += 1
                encontrado = True
                break
        if not encontrado:
            lista_frecuencias.append([palabra, 1])

   # Ordenar para poder elegir las 50 primeras
      # Primero hago una función que me dé la frecuencia (o sea, el número de veces)
    def obtener_frecuencia(elemento):
        return elemento[1]
    # Ahora sí, ordeno la lista de mayor a menor usando esa función
    lista_frecuencias.sort(key=obtener_frecuencia, reverse=True)

    print("Palabras más frecuentes:")
    top = 0
    for palabra, frecuencia in lista_frecuencias:
        print(palabra, ":", frecuencia)
        top += 1
        if top == 50:
            break


    

with open("archivo.txt") as archivo:
    contenido = archivo.read()

vocales, consonantes = contar_vocales_consonantes(contenido)
print("Vocales:", vocales)
print("Consonantes:", consonantes)

palabras_mas_frecuentes(contenido)
```
Según esto, entonces
````
Vocales: 1597835
Consonantes: 2612121
Palabras más frecuentes:
from : 18126
by : 18028
with : 12756
id : 12607
dec : 9267
nov : 8988
for : 7714
esmtp : 7188
oct : 4164
you : 3621
murder : 3594
smtp : 3594
to : 2767
the : 2544
svn : 2528
modify : 1884
new : 1877
this : 1877
message : 1839
was : 1834
sakai : 1823
at : 1822
using : 1821
can : 1821
set : 1812
my : 1811
source : 1807
notification : 1806
how : 1802
server : 1801
sent : 1800
receive : 1798
workspace : 1798
cmu : 1797
sieve : 1797
innocent : 1797
automatic : 1797
collab : 1797
notifications : 1797
sender : 1791
apache : 1790
jan : 1310
in : 951
thu : 791
tue : 751
fri : 639
mon : 607
u : 604
wed : 589
merge : 576
````
BIOGRAFIA  
Bibliografía
Maldonado, R. (2024a, diciembre 16). str.isalnum(): ¿qué es y cómo funciona el método en Python? KeepCoding Bootcamps. https://keepcoding.io/blog/que-es-el-metodo-str-isalnum-en-python-y-uso/

Maldonado, R. (2024b, diciembre 16). str.isalpha(): aprende a usarlo en tus proyectos de Python. KeepCoding Bootcamps. https://keepcoding.io/blog/que-es-str-isalpha-en-python-y-como-usarlo/

Python string endswith() method. (s/f). W3schools.com. Recuperado el 13 de julio de 2025, de https://www.w3schools.com/python/ref_string_endswith.asp

Python string isdigit() method. (s/f). W3schools.com. Recuperado el 13 de julio de 2025, de https://www.w3schools.com/python/ref_string_isdigit.asp

Python string isspace() method. (s/f). W3schools.com. Recuperado el 13 de julio de 2025, de https://www.w3schools.com/python/ref_string_isspace.asp

Python string istitle() method. (s/f). W3schools.com. Recuperado el 13 de julio de 2025, de https://www.w3schools.com/python/ref_string_istitle.asp

Python string startswith() method. (s/f). W3schools.com. Recuperado el 13 de julio de 2025, de https://www.w3schools.com/python/ref_string_startswith.asp

(S/f-a). Thedataschools.com. Recuperado el 13 de julio de 2025, de https://thedataschools.com/python/strings/islower-metodo-string.html

(S/f-b). Thedataschools.com. Recuperado el 13 de julio de 2025, de https://thedataschools.com/python/strings/isupper-metodo-string.html  
https://www.tutorialspoint.com/python/python_url_processing.htm#:~:text=urlunparse(partes),Esto%20devuelve%20una%20URL%20equivalente.
