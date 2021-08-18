# **Apuntes del curso de Git y GitHub** por Platzi

Estos son apuntes de autoria propia, junto a algunos extraidos del **curso de Git y GitHub** tomados en Platzi, podras ver aqui una colección de comandos de consola, y pasos para implementar funcionalidades de Git y GitHub.
Importante remarcar que para mis curso y para mis proyectos personales, hago haciendo uso de **WSL** en Windows 10 _Windows Subsystem for Linux_, asi que los comando usados en este cursos funcionaran en **WSL** y **Linux Ubuntu**, a menos que se remarque lo contrario.

Si deseas ver el proyecto de blog en html y css de este repositorio desplegado, podras encontrarlo aqui: [azthery.github.io/curso-git/](azthery.github.io/curso-git/)

## **Comandos de git**:

- **git init** Inicializa git en el directorio actual

- **git status** Nos muentra nuestro estado actual

- **git add** Agregamos un archivo o un grupo de archivo

- **git commit** Envita los cambios al repositorio

- **git commit -m "comentario"** Agregamos un comentario, esta es una buena practica

- **git config** configurar git

- **git config --list** para ver las configuraciones por defecto de mi git

- **git config --list --show-origin** para ver donde estan ubicadas las configuraciones

- **git config --global user.name "Nombre"** cambiar el nombre de usuario de git

- **git config --global user.email "Email"** cambiar el nombre de email de git

- **git log archivo** usar para ver datos del archivo, como quien lo creo, cuando, y sus versiones anteriores.

## **Comando mas avanzados**

- **git show archivo** esto nos mostrara los cambios actuales realizados sobre un archivo

Si queremos comparar dos versiones diferentes de un archivo debemos de hacerle `git log` al archivo, nos mostrara todas las versiones del este archivo, con el respectivo codigo de cada commit, usaremos estos codigo con `git diff`

- **git diff codCommit1 codCommit2** comparamos el commit1 con el commit2

>- **git branch** nos permite crear una nueva rama
>
>- **git checkout** nos permite movenos entre `branch`

___________________________________________


## **git log utiles**

- `git log --oneline ` Te muestra el id commit y el título del commit.
- `git log --decorate` Te muestra donde se encuentra el head point en el log.
- `git log --stat ` Explica el número de líneas que se cambiaron brevemente.
- `git log -p` Explica el número de líneas que se cambiaron y te muestra que se cambió en el contenido.
- `git shortlog ` Indica que commits ha realizado un usuario, mostrando el usuario y el titulo de sus commits.
- `git log --graph --oneline --decorate y`
- `git log --pretty=format:"%cn hizo un commit %h el dia %cd" ` Muestra mensajes personalizados de los commits.
- `git log -3 ` Limitamos el número de commits.
- `git log --after=“2018-1-2”`  Commits para localizar por fechas
- `git log --after=“today” y`    Commits para localizar por fechas
- `git log --after=“2018-1-2” --before=“today” ` Commits para localizar por fechas.
- `git log --author=“Name Author” ` Commits realizados por autor que cumplan exactamente con el nombre.
- `git log --grep=“INVIE” ` Busca los commits que cumplan tal cual está escrito entre las comillas.
- `git log --grep=“INVIE” –i` Busca los commits que cumplan sin importar mayúsculas o minúsculas.
- `git log – index.html` Busca los commits en un archivo en específico.
- `git log -S “Por contenido”` Buscar los commits con el contenido dentro del archivo.
- `git log > log.txt ` guardar los logs en un archivo txt

___________________________________________


## **Conectar nuestro repositorio local con GitHub**

>Desde el 1 de octubre del 2020, GitHub cambio el nombre de la rama principal por defecto de "master" a "main", ya que esto estos nombres se de caracter ofennsivos, los cuales no debemos de seguir genarizando
>Sin embargo Git no ha hecho estos cambios y estos pueden generar algunos problemas, para ellos en nuetro repositorio local podemos cambiar `branch` local por "main", en remoto por "master".

Para conectar nuestro repositorio en local, con uno remoto ya creado en GitHub, debemos de ingresar el siguiente comando
```
git remote add origin URL
```
Donde URL es el link en `https` del repositorio en **GitHub**

Una vez hecho esto debemos de traernos el repositorio en **GitHub**, 
para ello debemos
```
git pull origin master
```

sin embargo **git** nos lanzara una **advertencia** un _warning_, ya que este se "rehusara a fusionar historias no relacionadas", sin embargo podemos forzar a que lo haga de la siguiente manera
```
git pull origin master --allow-unrelated-histories
```
Con esto ya tendremos sincronizado nuestro repositorio local, con nuestro repositorio remoto en GitHub.

Algo que tenemos que tener en cuenta, es que desde GutHub podemos realizar cambios al los documentos _(a este mismo por ejemplo)_, y cada vez que queramos guardar este cambio realizaremos un **commit** al repositorio remoto de GitHub, sin embargo el repositorio local no cambiara.
Tambien en el caso que estemos trabajando con mas persona en el mismo repositorio local y alguien haya agregado algún cambio.
Para actualizar nuestro repositorio local debemos ejecutar en consola:
```zsh
git pull origin master
```
>No olvida que debemos de realizar esta accion con cuidado por que podemos llegar a perder cambios realizados en el respositorio local.

___________________________________________

## **Llaves publicas y privadas**

Si queremos enviar un mensaje "secreto", no basta con solo darle una constraseña, ya que la misma contraseña podria ser capturada.
Para ellos existen las llaves publicas y privadas:

- Llave publicas: Estas se las **puedes compartir a cualquiera**, ya que esta la envias al remitente para este codifique el mensaje
- Llave privadas: Estas la usas para descodificar el mensaje que te han enviado, **esta es privada y no debe de ser compartida**

___________________________________________


## **SSH o Secure Shell**
Es un protocolo de red que permite acceso remoto seguro a través de una conexión encriptada. Este método de autenticación requiere un passphrase (contraseña) o tambien puede funcionar sin passphrase sobre la clave.

En el directorio **Home** ~

```zsh
git config -l
```
Muestra la configuración dentro de Git(user y email), Este comando funciona por que Git esta instalado en todo el equipo local.

```zsh
$ git config --global user.email “nombre_email_cambiado”
```
Se puede utilizar este mismo comando para cambiar el email.

**Creamos la llave SSH**
```zsh
ssh-keygen -t rsa -b 4096 -C "tu_email@gmail.com"
```
1. **-t** = Especifica cual es el algoritmo que vamos a usar para crear esa llave.
2. **rsa** = Algoritmo a usar, hasta el momento el mas popular.
3. **-b** = Especifica que tan compleja es la llave.
4. **4096** = Complejidad de la llave desde una perspectiva matemática.
5. **-C** = Indica a que correo electrónico va estar conectado esta llave
6. **"tu_email@gmail.com"** = Correo electrónico.

>Guardar la llave en la dirección predeterminada.
>
>Passphrase: Password con espacios o Contraseña adicional de texto que le vas a poner a tu llave pública y privada.

### **1er Paso:**
Una ves que tengamos la llave, tenemos que agregarlo al entorno, y el entorno es básicamente que el sistema operativo donde tu trabajas sepa que la llave existe. Para ello ejecutamos lo sgte:

revisar el servidor de llaves / Evalúa que un comando se dispare.
```
eval $(ssh-agent -s)
```
>**Agent pid 4724**
>
>Agent = Significa que el servidor de SHH esta corriendo.
>
>pid = Process id o identificador del proceso.
>
>4724 = Número que al sistema operativo le dice que el proceso esta corriendo.

### **2do Paso:**

Agregamos la llave privada a nuestro sistema o al servidor por que no basta con que la llave solo exista, sino debemos decirle que existe. Para ello ejecutamos el siguiente comando:
```zsh
ssh-add ~/.ssh/id_rsa
 ```

>- ~ = Home
>- .ssh = carpeta ssh
>- id_rsa = llave privada la que nunca debemos de mostrar.

__________________________________________________________

## **Conectar reposittorio local con GitHub**

Primero debemos ubicarnos en la capeta **home**, para esto en mac debemos de:
```zsh
~
```
Aqui podemos ubicar la carpeta _(por default)_, la cual es **.ssh**
```zsh
.ssh/
```
para confirmar de que los archivos se encuentran aqui escribimos
```zsh
ls -al
```

Una vez ubicado los archivos, ya podremos agregarlos, escribiendo lo siguiente en consola:
```zsh
ssh-add ~/.ssh/ad_rsa
```
>Con esto agregamos nuestra **llave publica** o _public key_

### **Agregando nuestro proyecto actual**

Una vez hecho la anterior podemos diriginos al proyecto actual, una vez ahi cambiaremos nuestra **URL**, pero primero le daremos un vistazo a la actual con el comando
```zsh
git remote -v
```
Ahi podremos ver la **URL** actual, ahora bien debemos dirigirnos al repositorio en GitHub, ir al repositorio remoto y hacer lo siguiente:
1. Preionar el boton verde de **Code**
2. Seleccionar **SSH**
3. Copiar esa **URL**

Esta URL la agregaremos al repositorio local de la siguiente manera
```zsh
git remote set-url origin URL
```
- **URL**: Es la URL copiada en GitHub

Una vez hecho esto por **buenas practicas**, haremos un `git pull` para verificar si todo esta bien y sincronizar cambios.
```
git pull
```
y luego nos preguntara si confiamos en la pagina "github.com" si deseamos continuar, le ingresaremos que
```
yes
```
Y con esto podremos proseguir a darle `git commit` y `git push`.

_____________________________________________________

## **Tags y versiones**

**Alias**: es una forma de guardar codigo que se nos haria muy largo y facilmente olvidable, en una variable corta de nuestra autoria.
Osea es practicamente guardar un comando en consola como si fuera una variable string, lo haremos con un ejemplo, guardaremos el comando:
```zsh
git log --all --graph --decorate --oneline
```
Y ahora lo agregaremos al alias **arbolito**
```zsh
alias arbolito="git log --all --graph --decorate --oneline"
```
y listo, ahora solamente escribiendo
```
arbolito
```
ejecutare su comando asignado.

### **Tags**
Nuestro repositorio guarda multiples versiones de nuestro desarrollo del proyecto, nosotros podemos **marca** **puntos** en ese desarrollo, como recordatorio o marcas, las cuales podemos darle utilidad en GitHub, al hace uso de nuestros tags podremos volver al punto deseado de manera prodigia y sencilla.

Para **crear** un **tag** debemos de indentificar primero el hush, para eso usaremos `arbolito`, debemos de copiar el Hush y usarlo en el siguiente comando

```zsh
git tag -a NombreDelTag -m "descripcion del tag" Hush
```
- **a-**: significa agregar un tag
- **NombreDelTag**: es el nombre que le daremos a este, por convensión se usa la v0.1 para la primera version
- **-m**: para enviar un mensaje como un `commit`
- **"descripcion del tag"**: es eso, una descripcion
- **Hush**: es el codigo de la versión a marcar


>Al realizar un `git status` luego de crear un tag, no aparecera ningun cambio, sin embargo igualmente habra que hacer un `git pull` y un `git push`

Al realizar un `git push` para **tags**, estos se le debe de hacer mediante su comando propio el cual es:
```zsh
git push origin --tags
```

### **Eliminar Tags**
Pero si por alguna razón necesitamos eliminar un tag podemos eliminarlo facilmente desde la **interfaz de GitHub** o con comandos en consola de la siguiente manera:
```zsh
git tag -d NombreDelTag
```
- **-d**: delete
- **NombreDelTag**: es el nombre del tag, bruh

>Para finalizar debemos de realizar el tipico `git pull` y `git push`
```zsh
git push origin --tags
```
### **Eliminar Tags para GitHub**
Sin embargo en GitHub no se eliminara los tags
> esto se debe ya que los tags es una manera para indicar que el producto ya esta listo

para eliminarlo de GitHub debemos de ejecutar el siguiente comando:
```zsh
git push origin :refs/tags/NombreDelTag
```

________________________________________________________________________

## **Branch**

Branch o _ramas_ nos permite divir en versiones palalelas de nuestro proyecto, para trabajar en diferentes "sitios" del proyecto de forma individual, asi facilitando el trabajar en colaboración.

Para **ver las ramas ejecutamos**:
```zsh
git branch
```

Para **crear** una **branch**:
```zsh
git branch nameBranch
```

Si queremos **ver todas las ramas** :
```zsh
git show-branch --all
```

Para **movernos entre branch**:
```zsh
git checkout nameBranch
```

Si queremos **enviar** nuestra **rama** al **repositorio**:
```zsh
git push origin nameBranch
```

**Eliminar branch localmente**:
```zsh
git branch -D nameBranch
```

**Eliminar branch en repositorio**:
```
git push origin --delete nameBranch
```

**Fusionar** o **meclezclar ramas**, para realizar lo siguiente es importante posicionarse primero en la rama "principal" a la cual le queremos llevar esos cambios al realizar el **merge**, luego ejecute el comando
```zsh
git merge nameBranch
```
Luego de esto nos pedira **escribir** un **comentario**.
Finalmente habra que ejecutar el tipico `git pull` y `git push`

_________________________________________________________________________

## **Collaborators**

GitHub al ser un repositorio remoto nos permite llevar a cabo proyectos colaborativos, esto quiere decir que nos permite desarrollar un proyecto con mutiples colaboradores.

Sin embargo **no cualquiera puede hacer un `push`**, ya que nuestro administrada(o) del repositorio debe de enviarnos una invitación.
Nosotros como admi de nuestro repositorio, para invitar a un colaborador, debemos de seguir los siguientes pasos:

1. Ir a nuestro repositorio.
2. Settings
3. Manage access
4. Invite a collaborator
5. ingresar el email o usarname de quien deseamos invitar

_________________________________________________________________________

## **Flujo de trabajo profesional con Pull requests**

Normalmente en entornos profesionales la **rama principal** _master o main_, se **bloquea** ya que esta rama se utiliza para alojar la version mas **estable** y **refinada** de nuestra app, es generalmente esta rama la cual es utilizada para enviar al **servidor** de la **pagina web** o a la **play store**.

Para realizar pruebas y llevar a cabo el desarrollo se usa normalmente la rama llamada **staging server**

### **Pull Request**

Es la acción de **validar** el **codigo** que se va a **mergear** de un rama a otra, osea es una **estancia** donde se **evalua** si este **codigo** pasara para ser para hacerle **merge**, o **necesita correción**.
Quienes llevan a cabo esta tareas normalmente son los lideres del equipo o un perfil denominados como **DevOps**.

>Pull request **no es una caracteristic**a de **Git**, si no de **GitHub**.

>Esta posee nombres diferentes para plataformas difetentes
>- **GitHub:** Pull request
>- **GitLab:** Merge request
>- **Bitbucket:** Pull request

### Pero, **¿Por que y para que existe Pull Request?**

Pull rquest es comparable con un control de calidad del codigo, es una manera de refinar el codigo en el proceso antes de mandarlo a nuestro producto, asi solucionando conflictos, problemas y bugs, lo cual nos ayuda a ahorrar tiempo y recursos a la hora de llevar a cabo el proyecto.

_________________________________________________________________________

## **Flujo de trabajo con Pull Request**

Al hacer un pull request se genera una conversación que pueden seguir los demás usuarios del repositorio, así como autorizar y rechazar los cambios.

El flujo d e trabajo es el siguiente:

1. Se trabaja en una rama paralela los cambios que se desean 
```zsh
git checkout -b <rama>
```
2. Se hace un commit a la rama 
```zsh
git commit -am "<Comentario>"
```
3. **Se suben al remoto los cambios**
```zsh
git push origin <rama>
```
4. En GitHub se hace el `pull request` comparando la **rama master** con la rama del **fix**.
5. Uno, o varios colaboradores revisan que **el código sea correcto** y dan **feedback** (en el chat del pull request).
6. El colaborador hace los cambios que desea en la **rama** y lo **vuelve a subir** al remoto (automáticamente jala la historia de los cambios que se hagan en la rama, en remoto).
7. Se **aceptan los cambios** en GitHub
8. Se hace **merge** a `master` desde GitHub

**Importante**: Cuando se modifica una `rama`, también se modifica el `pull request.`

>_Notas Escritas por Davidad Behar en Platzi_

_________________________________________________________________________

## **Forks o _Bifurcaciones_**

Es una característica única de GitHub en la que se crea una copia exacta del estado actual de un repositorio directamente en GitHub, éste repositorio podrá servir como otro origen y se podrá clonar (como cualquier otro repositorio), en pocas palabras, lo podremos utilizar como un git cualquiera.

Un fork es como una bifurcación del repositorio completo, tiene una historia en común, pero de repente se bifurca y pueden variar los cambios, ya que ambos proyectos podrán ser modificados en paralelo y para estar al día un colaborador tendrá que estar actualizando su fork con la información del original.

Al hacer un fork de un poryecto en GitHub, te conviertes en dueñ@ del repositorio fork, puedes trabajar en éste con todos los permisos, pero es un repositorio completamente diferente que el original, teniendo alguna historia en común.

Los forks son importantes porque es la manera en la que funciona el open source, ya que, una persona puede no ser colaborador de un proyecto, pero puede contribuír al mismo, haciendo mejor software que pueda ser utilizado por cualquiera.

Al hacer un fork, GitHub sabe que se hizo el fork del proyecto, por lo que se le permite al colaborador hacer pull request desde su repositorio propio.

### **Trabajando con más de 1 repositorio remoto**

Cuando trabajas en un proyecto que existe en **diferentes repositorios remotos** (normalmente a causa de un **fork**) es muy probable que desees poder **trabajar con ambos repositorios**, para ésto puedes crear un **remoto adicional** desde consola.
```zsh
git remote add <nombre_del_remoto> <url_del_remoto> 
```
```zsh
git remote upstream https://github.com/freddier/hyperblog
```

Al crear un **remoto adicional** podremos, hacer pull desde el nuevo **origen** (en caso de tener permisos podremos hacer fetch y push)
```zsh
git pull <remoto> <rama>
```
```zsh
git pull upstream master
```

Éste `pull` nos traerá los **cambios del remoto**, por lo que se estará al día en el proyecto, el flujo de trabajo cambia, en adelante se estará trabajando haciendo **pull desde el upstream** y **push al origin** para pasar a hacer **pull request**.

>_Notas Escritas por Davidad Behar en Platzi_

_________________________________________________________________________

## Ignorar archivos en el repositorio con **.gitignore**

**No todos los archivos deben de ser guardados** en el repositorio, siempre habra algunos que deban de ser **ignorados**, por razónes de seguridad, tipo de archivo, privacidad,  blob (binary large object, objeto binario grande), es `node_modules`, etc.

Para **evitar** que estos archivos se **guarden** en el **repositorio**, existe `.gitignore`.

[Syntax de .gitignore](https://git-scm.com/docs/gitignore)

Algunas sintaxis mas comunes son:
- **/dir/archive.js** : agregar la url del **directorio**
- __*.jpg__ : usando y un `*` junto con la `extención`, **ignorara** todos estos tipos de archivos

_________________________________________________________________________

**Readme.md y Markdown**, es una excelente práctica

`README.md` es un archivo que te vas a encontrar en la mayoria de repositorios, es un archivo en **MarkDown** `.md` similar a un `.txt` pero el cual tiene mayor capacidad de edición.

Es una buena practica utilizar el `README.md`, ya que en GitHub este sera visible en la pantalla de vista general del repositorio, en el cual generalmente se utiliza escribir la descripción del repositorio y/o la documentación, pero en si puedes utilizarlo para escribir lo que ti se te ocurra, como yo que lo utilizo para escribir los apuntes de esta curso.

>El archivo `README.md`, se escuenta en la raiz del repositorio

_________________________________________________________________________

## **Git Rebase**: reorganizando el trabajo realizado

`git rebase` reescribe la historia del repositorio, en donde originalmente fue cambios realizados en dos ramas, sera que todos esos cambios fueron hechos solo en una.
Es como si fuera un merge pero fusionando tambien sus historias.

Ralizar un `git rebase` es una **muy mala practica**, se debe de hace bajo circunstancias muy especificas y solo en el repositorio local.

Como utilizar `git rebase`:

1. Ubicarnos en la **rama** que **ira a desaparecer**.
2. **Usar** `git rebase <principal branch>`
3. Luego ubicarnos en la **rama principal**
4. Usar ahora `git rebase <experimental branch>`
5. (opciónal) eliminar rama experimental

_________________________________________________________________________

## Git Stash: Guardar cambios en memoria

`git stash` nos permite **guardar** en cambios hechos que aun no hemos mandados en un `commit`, en una especie de **"memoria alterna"**.
Esto nos puede ser de **gran utilidad en caso que querramos cambiar de rama** y no querramos aun hacer un `commit` los cambios, u cualquier otra utilidad que se nos ocurra.
Al hacer `stash` todos nuestros **cambios realizados se guardaran** y **volveremos a como estaba nuestra rama en nuestro anterior `commit`**

- Para hacer uso de `git stash`, **debemos de estar en la rama** con los cambios aun enviados y **ejecutar**:
```zsh
git stash
```
Si deseamos podemos **asignarle un mensaje al stash**
```zsh
git stash save "<mensaje>"
```

- Ver los **stash guardados**
```zsh
git statsh list
```

- Recuperar ultimo stash
```zsh
git stash pop
```

- Aplicar stash **especifico** y **eliminarlo**
```zsh
git stash pop stash@{<num_stash>}
```

- **Retomar** los cambios de una **posición específica** del Stash
```zsh
git stash apply stash@{<num_stash>}
```

- **Guardar** el stash en una **nueva rama**
```zsh
git stash branch <newBranch>
```

- **Eliminar stash mas reciente**
```zsh
git stash drop
```

- **Eliminar stash especifico**
```zsh
git stash drop stash@{<num_stash>}
```

- **Eliminar todos los stash**
```zsh
git stash clear
```