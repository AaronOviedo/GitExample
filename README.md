# *GitExample*
Veremos como manejar git, de una manera sencilla y apropiada para manejo simple de código y repositorios, además de algunas recomendaciones de buenas "praxis".

## Indice
    1.- Explicaciones básicas.
    2.- Commits
    3.- Repositorios remotos
    4.- Ramas
    5.- ¿Qué hacer cuando hay diferencias?
    6.- Stash.


## Explicaciones básicas
**¿Qué es git?**  
Es un systema de control de repositorios.

**Iniciar un repositorio**  
`git init`  

**Ver los cambios actuales y estatus de la rama**  
`git status`

**Clonar un repositorio**
`git clone` *`ruta_repositorio`*

**¿Cómo esta compuesto git?**  
Git esta compuesto por tres **"estados"** o ramas de trabajo.
- El lugar de trabajo: ***Working Space***
- El punto intermedio o index de cambios: ***Stage Space***
- El guardado de los commits: ***Head Space***  


## Commits
***Proceso de guardado de cambios***
Para agregar los cambios al repositorio, se necesita pasar por los tres estados. El primero, el lugar de trabajo, es al estar codificando, se estan registrando diferencias a los archivos.

Para guardar estos cambios, o "prepararlos" para ser guardados (continuar con el stage stage), se utiliza el comando:  
`git add .` - Para agregar todos los archivos a la vez (Se puede usar punto o asterisco). O en su defecto:  
`git add <filename>` - Para agregar un solo archivo.  
En este punto, todavía se puede evitar agregar un archivo al commit, o cambio. El comando para esto es:  
`git checkout <filename>` - Este comando quita del "stage space" el archivo indicado(tambien se puede usar en carpetas, y quita del stage todo dentro de la carpeta que esta en el stage).  

Por último, para guardar por fin los cambios, o tenerlos versionados, se hace un "commit". El comando para esto es:  
`git commit -m 'Mensaje o explicación de los cambios'` 

También se puede dejar únicamente con `git commit` y después el propio git te pide que agregues una descripción en el siguiente paso.

## Repositorios remotos
Al usar el comando `git init` se crea un repositorio "local". Es un repositorio que solo nosotros podemos ver. Los repositorios ***remotos*** al contrario, son almacenados en la nube para que más personas puedan accesar a ellos.

Al clonar un repositorio remoto, de forma automática se crea la relación con el local y el remoto. Generalmente por el nombre convencional de ***origin***.

Se pueden tener más un repositorio remoto conectado al local, pero no es recomendado.

Para ver estos repositorios se utiliza el comando:  
`git remote -v`  

Para agregar un nuevo repositorio remoto se utiliza el comando:  
`git remote add <nombre> <ruta_repositorio>`  

Y para remover los repositorios se utiliza el comando:  
`git remote rm <nombre>`  

Pero lo importante, es mandar los cambios hecho de manera local al repositorio, para que no se queden en la computadora personal y las demás personas con acceso puedan verlos. Esto se logra (después de haber hecho los pasos del commit) utilizando el comando:  
`git push <remoto> <rama>`  

Ahora para bajar los cambios se utiliza el comando:  
`git pull <remoto> <rama>`

## Ramas
Hablando de subir ramas. Las ramas son diferentes versiones del repositorio para cumplir un próposito en especifico. La rama principal y que se crea al iniciar cualquier repositorio se llama `master`.

Para crear nuevas ramas se utiliza el comando:  
`git checkout -B <rama>`  
Para cambiar entre ramas, se remueve la parte "-b" del comando.

Para conocer las ramas que existen localmente:  
`git branch`, y borrarlas se le agrega `-D <rama>`  

Lo importante de crear ramas, es que en algún punto tienen que converger. Para esto se hace un "merge" entre las ramas.
La sintaxis de esto es primero hay que posicionarse en la rama destino, y luego utilizar el comando:  
`git merge <rama_salida>`

## ¿Qué hacer cuando hay diferencias?
Se puede continuar y aceptar ambos cambios, se puede remover el merge, o se puede entrar al editor con el que se codifica y se hace un nuevo commit.  

Los comandos son, respectivamente:  
`git merge --continue`  
`git merge --abort`  
`git commit -am 'Merge conflicts'`

### Extra - Borrar commits o ir a un commit específico
Para borrar el último commit, por algún error o que se fue algo de más, o de menos. Se utiliza el comando:  

`git reset HEAD`  

En caso de encontrar un bug en una versión espécifica, y ver que fue lo que lo causo, o tenerlo en un ambiente "isolate". Primero se necesita saber el ID del commit, que es un código Hexadecimal.

Se consigue con el comando:  
`git log`  
Y para cambiar se utiliza el comando:  
`git checkout <ID>`

Por último, para borrar más de uno o no el último.  
`git rebase --onto <rama>~<primer_commit_borrar> <rama>~<commit_a_mantener> <rama>`

## Stash
Stash es un comando que guarda los cambios actuales, en una pila, para ser usados después, sin hacer un commit. (El equivalente a un shelvset). Y luego borra los cambios hasta dejarlo equivalente hasta el último commit.

Los comando son:
`git stash push` - O solo escribir `git stash`, hacen el mismo trabajo.  
`git stash pop` - Trae el último stash de la pila; si se le agrega `--index` se selecciona uno en especifico.  
`git stash apply` - Lo mismo que pop, pero no lo borra de la pila.
`git stash list` - Muestra todos los stash.