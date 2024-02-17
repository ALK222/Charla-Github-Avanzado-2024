::: frame
Tabla de contenidos
:::

# Introducción

::: frame
Introducción

Charla anterior:
<https://github.com/ALK222/charla-git-principiantes-2023>

Se asume que:

-   Tenéis cuenta de GitHub

-   Sabéis hacer crear repositorios

-   Sabéis hacer *commit*, *push*, *pull*
:::

# Ramas

::: frame
Ramas

-   Mantienen el desarrollo paralelo para distintas partes del programa

-   Mantienen separadas las versiones estables de las de desarrollo

-   Nos permiten proteger ciertas ramas
:::

::: frame
![origen de la imagen:
<https://stackoverflow.com/questions/46827112/toggling-branch-tree-view-in-gitkraken>](Images/ejemplo-ramas.png){width="70%"}
:::

## Main

::: frame
Main

La rama Main (en proyectos antiguos también se puede encontrar como
Master) es la rama principal del proyecto y la primera rama que se crea
automáticamente al crear el repositorio.

-   Rama (normalmente) protegida para evitar código malicioso (de manera
    intencional o no) sin supervisión.

-   Generalmente es la rama estable del programa, solo se suben
    versiones definitivas
:::

## Ramas secundarias

::: frame
Ramas secundarias A estas ramas les daremos nosotros un nombre al
crearlas. Son útiles para desarrollar nuevas características del
programa o para hacer arreglos de bugs.

Estas ramas se pueden unir a la principal en cualquier momento del
desarrollo para incorporar estos cambios a la rama principal.
:::

## Pull request y Merge

::: frame
Merge

Un *Merge* nos permite unificar un conjunto de *commits* en un solo
historial.

Normalmente esto se hace entre los extremos de dos ramas para
fusionarlas en una sola.

Esto puede generar conflictos entre archivos que se pueden resolver con
distintos editores de texto o herramientas de gestión de git.
:::

::: frame
Pull Request

Un *pull request* es un mecanismo de GitHub para poder hacer *merge* en
proyectos ajenos o para solicitar feedback antes de hacer un merge en tu
propio proyecto.

En ciertos repositorios es obligatorio pasar una *pull request* con
varios supervisores para poder contribuir si no eres parte del equipo.
:::
