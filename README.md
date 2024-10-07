<div align="right">
<img width="32px" src="img/algo2.svg">
</div>

# TP1

## Alumno: Laura Maciel - 111415 - lamaaciel@fi.uba.ar

- Para compilar:

```bash
make tp1
```

- Para ejecutar:

```bash
make tp1
```

- Para ejecutar con valgrind:
```bash
make valgrind-tp1
```

---

##  Funcionamiento del TP1.c

El programa implementa una Pokedex simple utilizando un archivo CSV como fuente de datos. El funcionamiento general del mismo se puede resumir en los siguientes pasos:

1. Verifica los argumentos de línea de comando.
2. Abre el archivo CSV especificado.
3. Crea una nueva Pokedex.
4. Lee el archivo CSV línea por línea, parseando cada línea para crear un nuevo Pokémon.
5. Agrega cada Pokémon a la Pokedex.
6. Itera sobre la Pokedex para imprimir todos los Pokémon y contar los tipos.
7. Libera la memoria y cierra los recursos.

### Análisis de Complejidad Temporal
```c
parseoNombre, parseoTipo, parseoInt: O(1) - Operaciones simples de conversión.
imprimirPokemon: O(1) - Imprime un Pokémon en tiempo constante.
contarPokemonPorTipo: O(1) - Incrementa un contador basado en el tipo.
main: O(n), donde n es el número de líneas en el archivo CSV.

La lectura del archivo y la adición de pokemones a la Pokedex dominan la complejidad.
Cada operación de agregar a la Pokedex es O(k), donde k es el número actual de pokemones, en el peor de los casos, resulta en una complejidad O(n^2) en main.
```

##### Nota relativamente importante sobre el tp:
**En esta pokedex no se utiliza una estructura con indice estático y los pokemon pueden ser duplicados**

### Manejo de Memoria
 -> Se asigna memoria dinámicamente para cada nombre de Pokémon.
 -> Se mantiene un array nombres_asignados para facilitar la liberación de memoria al final.
 -> Se utiliza realloc para expandir nombres_asignados cuando es necesario.
 -> Toda la memoria asignada se libera al final del programa.

Incluír **EN TODOS LOS TPS** los diagramas relevantes al problema (mayormente diagramas de memoria para explicar las estructuras, pero se pueden utilizar otros diagramas si es necesario).

### Digrama de memoria de TP1.c:
Diagrama que muestra el estado durante la lectura y procesamiento del archivo CSV.

<div align="center">
<img width="70%" src="img/maxUsoTp1.png">
</div>

##  Funcionamiento de csv.c

csv.c contiene funcionalidades para trabajar con archivos CSV. Sus principales funciones son:

1. abrir_archivo_csv: Abre un archivo CSV y crea una estructura para manejarlo.
2. leer_linea_csv: Lee una línea del archivo CSV, la divide en campos y aplica funciones de parseo a cada campo.
3. cerrar_archivo_csv: Cierra el archivo CSV y libera la memoria asociada.

### Análisis de Complejidad Temporal
```c
abrir_archivo_csv: O(1) - Operaciones de apertura de archivo y asignación de memoria.

leer_linea_csv: O(k), donde k es la longitud de la línea a leer. En esta funcion, la complejidad es dominada por dividir_string ya que debe recorrer toda la línea.

cerrar_archivo_csv: O(1) - Operaciones de cierre de archivo y liberación de memoria.
```
### Manejo de Memoria
 -> abrir_archivo_csv asigna memoria para la estructura archivo_csv.
 -> leer_linea_csv asigna memoria temporalmente para la línea leída y para la estructura Partes. Al final libera la memoria de linea_leida
 -> Toda la memoria asignada al archivo se libera  en cerrar_archivo_csv.

### Digrama de memoria de csv.c:
Diagrama de estado de memoria al abrir_archivo_csv:
<div align="center">
<img width="70%" src="img/abrirArchivoCsv.png">
</div>

Diagrama de estado de memoria para leer_linea_csv:
<div align="center">
<img width="70%" src="img/leerLineaCsv.png">
</div>

##  Funcionamiento de pokedex.c

pokedex.c implementa la estructura de datos Pokedex y sus operaciones asociadas:

1. pokedex_crear: Crea una nueva Pokedex vacía.
2. pokedex_agregar_pokemon: Agrega un nuevo Pokémon a la Pokedex, manteniendo el orden alfabético.
3. pokedex_cantidad_pokemones: Devuelve el número de Pokémon en la Pokedex.
4. pokedex_buscar_pokemon: Busca un Pokémon por nombre.
5. pokedex_iterar_pokemones: Itera sobre todos los Pokémon en la Pokedex.
6. pokedex_destruir: Libera toda la memoria asociada a la Pokedex.

### Análisis de Complejidad Temporal
```c
pokedex_crear: O(1) - Asignación de memoria simple.
pokedex_agregar_pokemon: O(n), donde n es el número de Pokémon en la Pokedex.
    En el peor caso, necesita desplazar todos los Pokémon para mantener el orden.
pokedex_cantidad_pokemones: O(1) - Retorna un valor almacenado.
pokedex_buscar_pokemon: O(n) - Búsqueda lineal en el array de Pokémon.
pokedex_iterar_pokemones: O(n) - Itera sobre todos los Pokémon una vez.
pokedex_destruir: O(n) - Libera la memoria de cada Pokémon y de la Pokedex.
```
### Manejo de Memoria
 -> pokedex_crear asigna memoria para la estructura Pokedex.
 -> pokedex_agregar_pokemon usa realloc para expandir el array de Pokémon y copiar_cadena para el nombre.
 -> pokedex_destruir libera la memoria de todos los nombres de Pokémon y de la estructura Pokedex.

 ### Digrama de memoria de pokedex.c:
Estado de memoria luego de agregar un par de pokemones:
<div align="center">
<img width="70%" src="img/pokedexMem.png">
</div>