# **Apuntes del curso de Git y GitHub** por Platzi

Estos son apuntes de autoria propia, junto a algunos extraidos del curso de Git y GitHub tomados por mi en Platzi, aqui podras ver una colección de comandos en consola, y pasos para implementar funcionalidades.
Importante remarcar que para mis curso y para mis proyectos personales, estoy haciendo uso de WSL en Windows 10 _Windows Subsystem for Linux_, asi que los comando usados en este cursos funcionaran en WSL y Linux ubuntu, a menos que se remarque lo contrario.

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