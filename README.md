# **Apundes del curso de Git y GitHub** por Platzi
Este es un repositorio de practica para el curso de Git y GitHub de platzi

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

## **Conectar nuestro repositorio con GitHub**

Para conectar nuestro repositorio en local, con uno remoto ya creado en GitHub, debemos de ingresar el siguiente comando
```
git remote add origin URL
```
Donde URL es el link en `http` del repositorio en **GitHub**

Una vez hecho esto debemos de traernos el repositorio en **GitHub**, 
para ello debemos
```
git pull origin master
```

sin embargo **git** nos lanzara una **advertencia** un _warnning_, ya que este se "reusara a fusionar historias no relacionadas", sin embargo podemos forzar a que lo haga de la siguiente manera
```
git pull origin master --allow-unrelated-histories
```

