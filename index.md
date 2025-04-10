---
author:
- Alejandro Barrachina Argudo
date: 2024
subtitle: Ramas, comunicación, workflows
title: Charla GitHub avanzado 2024
---

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
<https://stackoverflow.com/questions/46827112/toggling-branch-tree-view-in-gitkraken>](../Images/ejemplo-ramas.png){width="70%"}
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

Tras una *pull request* se hace un merge entre dos ramas.
:::

::: frame
Fork

Un *fork* es un nuevo repositorio que comparte visibilidad y código con
un repositorio original.

Nos permite hacer modificaciones a un código ya existente y después
mover esos cambios al repositorio original con una *pull request* (o
no).
:::

## Submódulos

::: frame
Submódulos En el desarrollo de un proyecto, a veces necesitamos otras
herramientas o proyectos dentro. Una manera de gestionar esto desde git
es el uso de submódulos

Esto nos permite modularizar el desarollo, mantener todas las
herramientas actualizadas de manera sencilla y poder trabajar en
distintas partes del proyecto de manera independiente.
:::

::: frame
Para incluir un submódulo en un proyecto, usamos el comando:

<figure>
<pre style="custombash"><code>git submodule add &lt;url&gt; &lt;ruta del submódulo&gt;</code></pre>
</figure>
:::

# Workflows / Actions

::: frame
Workflows / Actions

Github actions es una plataforma de automatización para IC/CD que nos
permite crear flujos de trabajo y automatizar pruebas.

Gratis para repositorios públicos, de pago para repositorios privados
(2000[^1] minutos gratis y 500 MB gratis al mes).
:::

## Archivos

::: frame
Archivos

Los archivos para github workflows se guardan en la carpeta
**.github/wokrflows**.

Estos archivos son de formato *yml*
:::

## Estructura básica

::: frame
Estructura básica

Estos archivos siempre tienen que empezar con un nombre para el
proceso:\

<figure>
<div class="sourceCode" id="cb1" data-firstline="1" data-lastline="1"
style="customyaml"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="fu">name</span><span class="kw">:</span><span class="at"> Build LaTeX document</span></span></code></pre></div>
</figure>

Después definimos cuando ejecutar esta acción, puede hacerse en
distintas interacciones:

<figure>
<div class="sourceCode" id="cb1" data-firstline="2" data-lastline="2"
style="customyaml"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="fu">on</span><span class="kw">:</span><span class="at"> </span><span class="kw">[</span><span class="at">push</span><span class="kw">,</span><span class="at"> pull_request</span><span class="kw">]</span></span></code></pre></div>
</figure>
:::

::: frame
Estructura básica

Tras los pasos iniciales, empezamos con los "trabajos". Los trabajos
serán todas las cosas que van a ejecutarse dentro de esta acción. Estos
trabajos tendrán un nombre expresado como una variable, un entorno de
trabajo y una serie de pasos:\

<figure>
<div class="sourceCode" id="cb1" data-firstline="3" data-lastline="6"
style="customyaml"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="fu">jobs</span><span class="kw">:</span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a><span class="at">  </span><span class="fu">build_latex</span><span class="kw">:</span></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">runs-on</span><span class="kw">:</span><span class="at"> ubuntu-latest</span></span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a><span class="at">    </span><span class="fu">steps</span><span class="kw">:</span></span></code></pre></div>
</figure>
:::

::: frame
Estructura básica Cada paso tendrá un nombre, un componente que usa para
trabajar y posibles variables (dependen del componente):

<figure>
<div class="sourceCode" id="cb1" data-firstline="13" data-lastline="18"
style="customyaml"><pre class="sourceCode yaml"><code class="sourceCode yaml"><span id="cb1-1"><a href="#cb1-1" aria-hidden="true" tabindex="-1"></a><span class="at">      </span><span class="kw">-</span><span class="at"> </span><span class="fu">name</span><span class="kw">:</span><span class="at"> Upload PDF</span></span>
<span id="cb1-2"><a href="#cb1-2" aria-hidden="true" tabindex="-1"></a><span class="at">        </span><span class="fu">uses</span><span class="kw">:</span><span class="at"> actions/upload-artifact@v4</span></span>
<span id="cb1-3"><a href="#cb1-3" aria-hidden="true" tabindex="-1"></a><span class="at">        </span><span class="fu">with</span><span class="kw">:</span></span>
<span id="cb1-4"><a href="#cb1-4" aria-hidden="true" tabindex="-1"></a><span class="at">          </span><span class="fu">name</span><span class="kw">:</span><span class="at"> presentacion.pdf</span></span>
<span id="cb1-5"><a href="#cb1-5" aria-hidden="true" tabindex="-1"></a><span class="at">          </span><span class="fu">path</span><span class="kw">:</span><span class="at"> ./presentacion/Presentacion.pdf</span></span>
<span id="cb1-6"><a href="#cb1-6" aria-hidden="true" tabindex="-1"></a><span class="at">          </span><span class="fu">if-no-files-found</span><span class="kw">:</span><span class="at"> error</span><span class="co"> # &#39;warn&#39; or &#39;ignore&#39; are also available, defaults to `warn`</span></span></code></pre></div>
</figure>
:::

## Usos

::: frame
Usos

Estas acciones se pueden usar para automatizar pruebas, hacer versionado
de programas, subir archivos o incluso para [jugar al
ajedrez](https://github.com/marcizhu/marcizhu).

En el [marketplace](https://github.com/marketplace?type=actions) hay
miles de acciones ya desarrolladas para hacer casi de todo.
:::

# Repositorios especiales

::: frame
Repositorios especiales

Github se reserva el nombre de ciertos repositorios para crear lo que se
denominan "repositorios especiales".

Estos nombres son tu nombre de usuario y tu nombre de usuario seguido de
".github.io". El primero crea una descripción que se verá en la portada
de tu perfil, el segundo creará una página web principal para tu perfil
de github.
:::

# Github Pages

::: frame
Github pages

GitHub pages es un servicio de GitHub que nos permite alojar páginas
estáticas bajo el dominio "github.io".

Estas páginas se pueden hacer en cualquier repositorio, posicionarse en
distintas ramas y tener dos directorios fuente, la raíz del repositorio
o una carpeta "/docs"
:::

::: frame
![Opciones de GitHub pages antes de publicar la
página](../Images/github_pages.png){width="70%"}
:::

::: frame
![Opciones de GitHub pages después de publicar la
página](../Images/github_pages_deploy.png){width="70%"}
:::

## Jekyll

:::: frame
Jekyll

Estas páginas de github están construidas con Jekyll, permitiéndonos
esto hacer pruebas en local, usar HTML o markdown y utilizar todos los
plugins disponibles para Jekyll

::: columns
![image](../Images/jekyll.png){width="40%"}
:::
::::

::::: frame
Fin

:::: tcolorbox
::: columns
Alejandro Barrachina\
alejba02@ucm.es\
github.com/alk222
:::
::::

![image](../Images/qr_code.png){width="20%"}
:::::

[^1]: Minutos de uso en procesos linux, los procesos en Windows cuentan
    2x y en MacOs 10x
