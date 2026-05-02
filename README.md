# Introduccion a Git y github 

## Configurando git

---
1. Lo primero que hay que hacer es ir a la consola de git  bash como administrador
2. Vamos acceder a las configuraciones de git globales accediendo al name y el email

```bash 
    git config --global user.name "user cualquiera" 
```

```bash
    git config --global user.email "email cualquiera"
```

3. Luego vamos a ver todas las configuraciones de git

```bash
    git config --list
```

4. Y para ver las configuraciones globales 

```bash
    git config --global --list
```

5. Configurar visual studio code 

```bash 
    git config --global core.editor "code --wait"
```

6. configurar el colorizado para que git nos devuelva salidar mas coloridas

```bash 
    git config --global color.ul true
```

7. Sirve para manejar automaticamente los saltos de linea segun el sistema operativo | true si sos de windows | si sos de linux, mac input
   
```bash 
    git config --global core.autocrlf true
```

8. con esta configuracion cuando pongamos el git log --oneline lo que estamos es cortando la cantidad de hash sea el numero que sea 

```bash 
    git config --global core.abbrev 5
```

---

## Crear el primer repositorio 

---
Inicializar git

```bash 
    git init
```

preparar los cambios que queremos guardar

```bash 
    git add nombredelarchivo.html/js/jsx/tsx 
```

EL PUNTO SE CONSIDERA MALA PRACTICA A NO SER QUE ESTES MUY SEGURO DE LO QUE ESTES SUBIENDO

```bash 
    git add .
```

Git status nos muestra informacion sobre nuestro directorio de trabajo y el area de preparacion que vendria a ser .git

```bash 
    git status
```

Git rm lo que hace es sacar el archivo del area de preparacion  y no lo tiene en consideracion para un comit

```bash 
    git rm --cached archivo.html/css/js/jsx
```

Agregando el primer comit 

```bash 
    git commit -m "primeros comits" -a
```

Otra forma de subir un commit es asi, se te abriria una pestaña de visual studio code 
donde tenes que borrar todo y poner lo que hace el archivo y darle enter

```bash 
    git commit 
```

---

## Entendiendo los commits 

---
Si ponemos ejemplo un footer.html hacemos un git add y un commit, pero luego lo eliminamos para volver a recuperarlo es con git restore pero lo restauramos del area de preparacion porque ya lo habiamos subido se quedo ahi cuando yo lo habia eliminado del directorio local con restore lo devuelvo. O tambien te sirve para restaurar el archivo completo como fue commiteado la primera vez

```bash 
    git restore footer.html/js/jsx  
```

con un add el archivo queda listo para el commit el unstage lo quita de la preparacion para el commit 

```bash 
    git restore --staged footer.html/js/jsx  
```

El git checkout es como un viaje en el tiempo viaja hacia el commit que hiciste sobre el archivo y lo restaura como antes dejandote como los viejos cambios 

```bash 
    git checkout nombrearchivo.html/js/css
```

Ahora si modificamos un archivo, hacemos el git add de ese archivo y luego ponemos el git checkout no podemos volver atras porque ya esta en el area de preparacion. git reset esto descarta los cambios del repositorio y descarta los cambios en el area de preparacion

```bash 
    git reset --hard 
```

Es una forma mas simple de ver el git status con iconos:
-> M (rojo) que esta modificado pero no esta agregado
-> M (verde) que esta modificado pero agregado al area de preparacion 

```bash 
    git status -s
```

---

## Git giff

---
Show basicamente te muestra el contenido que esta en el commit, pero no te muestra lo que esta en el directorio o en el area de preparacion

```bash 
    git show nombrearchivo.html/css/js/jsx
```
Mostramos la diferencia de lo que esta en el area de preparacion con lo que esta en el commit primero tenemos que modificar el archivo luego hacer un git add
-El rojo es el que estaria en el commit 
-El verde es lo que esta en el area de preparacion

```bash 
    git diff --staged
```

Con esto visualizamos un control de registro de commits 

```bash 
    git log
```

Y con esto nos muestra un control de registro pero mas resumido 

```bash 
    git log --oneline
```

Con esto podemos comparar ambos commits mediante el hash del identificador compara lineas completas

```bash 
    git diff identificador1 identificador2
```

Con esta compara palabra por palabra 

```bash 
    git diff --word-diff identificador1 identificador2
```

---

## Commits 2 parte 

---

Esto sirve para modificar el nombre del ultimo commit que hicimos abriendo una pestaña del visual studio code

```bash 
    git commit --amend 
```

Con esto voy a tener la posibilidad de retroceder commits atras el numero 3 indica el numero de commits que estas regresando pueden ser mas o menos, se te abre una pestaña de visual studio code con los commits y colocar en el commit que quieras modificar en lugar de pick por edit. para hacer la agribilla con el teclado numerico es alt + 126 y guardamos con un amend. ADVERTENCIA esto vuelve al commit atras pero te borra los commits de adelante

```bash
    git rebase -i head~3
```
```bash
    git add home.html
```

```bash
    git commit --amend 
```

Con esto los commits que anteriormente se borraron de al hacer el rebase con esto se recuperan

```bash
    git rebase --continue 
```

Con esto borra el actual commit en el cual estas ejemplo si tenes v1, v2, v3, v4, v5
y vos estas en v5 lo borra y te deja en v4, por ende el commit eliminado se manda al area de preparacion 

```bash
    git reset --soft identificador
```

Con esto es igual la diferencia es que te puede borrar el numero de lo que vos quieras 

```bash
  git reset --soft head~1
```

Ahora con mixed vamos a borrar un commit, nuestro area de trabajo queda intacto en esos casos que tengamos archivos modificados o no modificados por ende el area de preparacion se limpiaria todo
  
```bash
  git reset --mixed identificador
```

despues tenemos hard que agarra el ultimo commit y borrarlo completamente y descarta los cambios de nuestro area de trabajo y agarra los archivos que estaban en ese commit que elimino y los pone en nuestro area de trabajo y descarta los cambios en nuestro area de preparacion

```bash
  git reset --hard identificador
```

--- 

## Ramas 

---
Para ver todas las ramas que tenemos creadas

```bash
  git branch
```

Para crear una rama se usa la nomenclatura kebabcase cabe destacar que al crear una rama tenemos sobre escrito el mismo proyecto como copia

```bash
  git branch modificar-home
```

para moverme a la rama que cree en este caso seria

```bash
  git switch modificar-home
```

Hacer todo en uno crear la rama + ya estar seleccionada

```bash
  git switch -c rama-nueva
```

Para borrar una rama, para borrar la rama hay que asegurarse de no estar en esa rama hay que salirse

```bash
  git branch -d rama-que-queres-borrar
```

Modificar el nombre de la rama 

```bash
  git branch -m nombre-de-la-rama nuevo-nombre-de-la-rama
```

Modificar el nombre de la rama estando en la rama misma

```bash
  git branch -m nombre-que-le-vamos-a-dar
```

Para que me muestra todos los comits estando en la rama master de todas las ramas

```bash
  git log --oneline --all
```

---

## Fusionar ramas Merge

---
Para fusionar ramas ejemplo de una rama creada a la master seria, cabe destacar que para que se fusione tengo que estar en la rama donde quiero que se fusione en este caso master o main

```bash
  git merge modificar-home 
```

---

## Git ignore
---
__*.txt__-> en este ejemplo gitignore ignoraria todo lo que termina con .txt puede ser tambien env, js, jsx etc etc
__!readme.txt__-> en esto le estoy diciendo quizas ignora todos los .txt menos el readme.txt
__auth/__ -> aca le estoy diciendo ignora todo lo que contiene la carpeta auth ejemplo que este register, login etc
__!auth/register.jsx__ -> aca le estoy diciendo ignora todo lo de la carpeta menos el register.jsx

Tambien podemos personalizar un gitignore global sin necesidad de que cada proyecto creememos un gitignore se puede crear en el disco C ejemplo escritorio 

```bash
  git config --global core.excludesfile C:\Users\Usuario\Desktop\config\.gitignore_global
```

Con esto visualizamos que ignoro gitignore en la rama master o cualquier rama

```bash
  git ls-tree -r --name-only HEAD
```

---

## Alias 

---
El alias sirve para cuando tenemos comandos muy largos lo podemos configurar con un alias en el comando de ejemplo podemos poner cualquier comando de git ejemplo:
__log --oneline --graph --all --pretty=format:'%C(auto)%h%d %s %C(black)%C(bold)%cr'__

```bash
     git config --global alias.nombre-alias "comando de ejemplo"
```

---

## Git reflog

---
 Esto sirve cuando usamos un reset eliminando un commit basicamente perdemos la referencia y para recuperar ese commit por accidente hay que hacer reflog, que es un log que es como el head se fue moviendo a todos los lugares que el head apunto

```bash
     git reflog
```

Y lo recupero 

```bash
     git reset --hard "identificador"
```

---

## Git clone
---
Con git clone basicamente descargamos un repositorio remoto recomendable la opcion https y copiamos el link

```bash
     git clone "agregar https"
```
---


