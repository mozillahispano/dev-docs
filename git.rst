.. index:: git, github

.. _git-chapter:


Git y Github
============

A menos que tengas un buen motivo, deberías estar utilizando ``git``
y GitHub_ para el control de versiones.

Recursos sobre Git
------------------

Si no sabes sobre ``git`` o no lo has usado en equipo, ¡no temas!.
Existe una gran cantidad de sitios maravillosos para que te inicies
con ``git``. Nosotros recomendamos:

* Help.Github_ te puede ayudar a arrancar con ``git`` sin importar
  qué sistema operativo uses. Si no has usado GitHub_ antes, este es
  el curso perfecto. También contiene buena información sobre ``git``
  como tal.
* `Pro Git`_ es probablemente el mejor recurso sobre ``git`` que
  existe. Cubre practicamente todo lo que puedes llegar a necesitar,
  por lo que es ciertamente extenso. Sin embargo, es una excelente
  lectura para llegar a conocer los aspectos básicos o para usar como
  referencia. `Pro Git`_ es escrito por uno de los desarrolladores de
  GitHub_.
* Hay una `lista de recursos sobre git en StackOverflow`_ que contiene
  herramientas, tutoriales, guías de referencia, entre otros.

La próxima vez que comiences un proyecto, ¡usa ``git``/GitHub_!. 
Trabajar en algo por tu cuenta es diferente a trabajar con otros, pero
comenzar con los comandos básicos de ``git`` (clone, branch, merge)
hará que las cosas más avanzadas (múltiples orígenes, rebasing, ...)
tengan más sentido.

.. _Help.Github: http://help.github.com/
.. _`Pro Git`: http://progit.org/book/
.. _`lista de recursos sobre git en StackOverflow`: http://stackoverflow.com/questions/315911/git-for-beginners-the-definitive-practical-guide

Prácticas de uso de Git en Mozilla
----------------------------------

* Lee sobre el `modelo de git-flow`_. En Mozilla se trabaja de manera
  similar, exceptuando el uso de ``master`` como rama de desarrollo,
  ``prod`` como rama de producción, y ``bug-$BUG_NUMBER`` como ramas
  de funcionalidades. Una vez conoces ``git``, entender como manejar
  las ramas de manera eficiente permitirá mantener correcciones de
  errores y características diferentes en sus propuas ramas. Esto es
  **realmente maravilloso**, ¡especialmente en casos de regresiones!.
* Usamos ``git submodule`` para nuestras librerías. El artículo sobre
  `git submodules explicados`_ te ayudará a entender cómo funcionan.
* Frecuentemente usamos ``git rebase`` para combinar y corregir commits
  antes de mezclarlos con los repositorios originales. Esto ayuda a
  mantener la historia del repositorio limpia y a mejorar las revisiones
  de código. GitHub_ tiene un `buen artículo sobre rebase`_.

.. _`modelo de git-flow`: http://jeffkreeftmeijer.com/2010/why-arent-you-using-git-flow/
.. _`git submodules explicados`: http://longair.net/blog/2010/06/02/git-submodules-explained/
.. _`buen artículo sobre rebase`: http://help.github.com/rebase/

github.com/mozillahispano
-------------------------

Los nuevos proyectos para Mozilla Hispano deberían iniciarse en la
`cuenta de Mozilla Hispano`_.

Contacta a ``Nukeador`` si deseas añadir un proyecto. Normalmente lo
puedes encontrar en el canal **#mozilla-hispano** en IRC.

.. _`cuenta de Mozilla Hispano`: https://github.com/mozillahispano

Trabajando en algún proyecto
----------------------------

Para trabajar en un proyecto existente:

* Haz un fork en tu cuenta
* Crea una rama para tu trabajo
* Envía un pull request para revisión
* Mezcla tu commit con ``master``, que debería estar configurada para seguir ``origin/master``
* ``git push``
* Coloca un enlace al commit en el Bug o Issue relevante

Mensajes de Commit
~~~~~~~~~~~~~~~~~~

* Sigue estos lineamientos_
* Debería contener un resumen de 50 caracteres, con los detalles necesarios
  debajo
* Si se trata de un bug o issue, debería contener ``bug 1234`` en el resumen.

.. _lineamientos: http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html

Manteniento master sincronizado
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Seguramente querrás mantener tu rama ``master`` local sincronizada.
Típicamente harás un ``rebase`` de tus ramas con tu ``master`` para
luego enviar (``push``) tus cambios a ``origin/master``.

Vamos a asumir que has definido tu remota ``origin`` de la manera correcta
en GitHub_. Por ejemplo, para Zamboni_. ::

    origin	git@github.com:jbalogh/zamboni.git

.. _Zamboni: https://github.com/jbalogh/zamboni

Tu archivo ``.gitconfig`` debería entonces contener lo siguiente::

    [branch "master"]
        remote = jbalogh
        merge = master
        rebase = true

Haciendo la vida más fácil
--------------------------

Herramientas para Git
~~~~~~~~~~~~~~~~~~~~~

**shell**

Hay un repositorio de herramientas para git llamado git-tools_ que nos
pueden facilitar la vida. Este contiene scripts de shell y Python que
hacen cualquier tipo de magia.

.. _git-tools: https://github.com/davedash/git-tools

Como muestra:

* ``git here`` te permite saber cuál es la rama actual.
* ``git compare`` con las opciones apropiadas en ``git.config`` te dará
  una URL de comparación en  GitHub_ para tu rama, que permite observar
  las diferencias de los cambios que ya han sido enviados.
* ``git url`` con las opciones correctas en ``git.config`` te devolverá
  la URL al último commit en  GitHub_.

Coloca estas herramientas en tu ``path`` y luego haz un fork y crea tus
propias herramientas para compartir.

**vim**

fugitive.vim_ puede ser la mejor herramienta para Git y Vim de todos los
tiempos.

.. _fugitive.vim: https://github.com/tpope/vim-fugitive

Oh My Zsh
~~~~~~~~~

`Oh My Zsh <https://github.com/robbyrussell/oh-my-zsh>`_ es una colección
excelente de scripts de zshell que pueden hacer que tu ambiente de `zsh`
sea maravilloso. Comprende una colleción de plugins, incluyendo algunos para
``git`` y GitHub_.

Algunos de esos se solapan con ``git-tools``. Adicionalmente, al usar Oh My Zsh
puedes ver fácilmente la rama actual y su estado en el ``prompt``.

Por ejemplo::

    dash@awesomepants in ~/Projects/bootcamp/the_code/docs
    (bootcamp) ±                                                    on master!

Donde:

* ``bootcamp`` es el `virtualenv` activo.
* ``±`` significa que estoy en un repositorio ``git``.
* ``master`` es la rama actual.
* ``!`` indica que hay cambios sin enviar en la rama actual.

Viendo código de otras personas
-------------------------------

En algunas ocasiones vas a tener que probar código de otras personas localmente.
Si tienes un pull request o un commit de la otra persona, esto es lo que debes
hacer para ver su código::

    git remote add otro git@github.com:otro/repo.git
    git fetch otro
    git co otro/rama

.. note::

   * ``otro`` es la otra persona.
   * La primera línea define una *remota*. Una *remota* no es más que un
     alias para un repositorio.
   * La segunda línea descarga todos los commits de ``otro`` que aún no tienes
     localmente. Normalmente esto son solo commits, pero en teoría puede ser
     cualquier cosa.
   * En la tercera línea se hace un cambio a la rama de ``otro``. Si tienes el
     hash de un commit, puedes hacer ``git co $COMMIT_HASH``.

.. _GitHub: https://github.com/
