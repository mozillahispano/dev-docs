Como programar
==============

En general, sigue las mejores prácticas establecidas para cada lenguaje
llenando los posibles huecos con sentido común.

.. index:: code;guidelines

Lineamientos Generales
----------------------

* *El estilo importa*

  La manera como el código se alinea importa, porque el código es
  revisado, editado y publico. El código difícil de leer no está acorde
  con el espíritu del código abierto.

* *Consistencia*

  Si haces algo de cierta manera, debes ser capaz de justificarlo.
  No mezcles `camelCase` con `guiones_bajos` al menos que tengas
  una buena razón para hacerlo.

* *Sigue el código que te rodea*

  Si no sabes lo que haces intenta seguir lo que los demás han hecho.

.. index:: code;testing

Pruebas
^^^^^^^

En lenguajes y *frameworks* que proveen facilidades para pruebas,
**¡escribe pruebas!**.

Trabaja en tener 80% o más de cobertura, especialmente en:

* *Privacidad*: prueba que las cosas privadas son privadas.
* *Código muy usado*: por ejemplo, páginas iniciales o código en librerías.
* *Bugs re-abiertos*

Codificar pruebas toma más tiempo que hacer el código, debido a que
suelen definir la funcionalidad de los productos. Las pruebas son muy
valiosas porque nos permiten realizar cambios de manera rápida sin
miedo afectar las funcionalidades.

La otra mitad de las pruebas es la integración contínua. Deberíamos estar
corriendo nuestras pruebas en cada cambio realizado y ser capaces de decir
con certeza que el código es correcto hasta nuestro mejor conocimiento.

.. index:: code;python coding style

.. _python:

Python
------

Hacemos lo que otros en la comunidad de Python han establecido:

* Seguir el PEP8_.
* Hacemos pruebas usando check.py_ u otra utilidad que combine `pep8.py` y `pyflakes`.
* Seguimos las extensiones al PEP8_ de Pocoo_.


Sentencias de importación
^^^^^^^^^^^^^^^^^^^^^^^^^

Extendemos las sugerencias establecidas en el PEP8_ para sentencias de importación.
Estas mejoran sustancialmente la habilidad de conocer qué está y que no está disponible
en un módulo dado.

Importa solo un módulo por sentencia de importación::

    import os
    import sys

no::

    import os, sys

Separa los grupos de importes con una línea en blanco:
librería estándar; Django (o framework); módulos de terceros; e importes locales::

    import os
    import sys

    from django.conf import settings

    import pyquery

    from myapp import models, views

Alfabetiza tus importes, esto hará que tu código sea más fácil de escanear.
Observa lo terrible que es esto::

    import cows
    import kittens
    import bears

Con un orden sencillo::

    import bears
    import cows
    import kittens

Imports primero, ``from``-imports después::

    import x
    import y
    import z
    from bears import pandas
    from xylophone import bar
    from zoos import lions

Eso es muchísimo más fácil de leer que::

    from bears import pandas
    import x
    from xylophone import bar
    import y
    import z
    from zoos import lions


Por último, cuando se importen objetos dentro de tu espacio de nombres
desde un paquete, utiliza el orden ``CONSTANTES``, ``Clases``, ``variables``
de forma alfabética::

    from models import DATE, TIME, Dog, Kitteh, upload_pets

Si es posible, sería más fácil importar el paquete completo. Especialmente
en el caso de métodos esto ayuda a responder la pregunta "¿de dónde saliste ``tu``?"

Malo::

    from foo import you


    def my_code():
        you()  # espera, ¿esto está definido en este archivo?


Bueno::

    import foo


    def my_code():
        foo.you()  # ah ok...


El espacio en blanco importa
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Usa siempre 4 espacios para indentar, no 2. Esto mejora la legibilidad considerablemente.
* Nunca utilices tabulaciones, la historia ha demostrado que no podemos manejarlas.

Las comillas
^^^^^^^^^^^^

Usa comillas sencillas en vez de dobles o triples si puede representar una mejora::

    'esto es bueno'

    'esto \'es\' malo'

    "esto 'es' bueno"

    "esto es inconsistente, pero se acepta"

    """a veces 'esto' es "necesario"."""

    '''nadie hace esto realmente'''


.. _PEP8: http://www.python.org/dev/peps/pep-0008/
.. _check.py: https://github.com/jbalogh/check
.. _Pocoo: http://www.pocoo.org/internal/styleguide/


.. index:: code;django coding style

Django
------

Sigue las recomendaciones para :ref:`python`. Hay algunas cosas en Django que
harán tu vida más fácil:

Usa ``resolve('myurl')`` y ``{{ url('myurl') }}`` cuando hagas enlaces
a URLs internas. Esto manejará automáticamente hosts, nombres relativos
y rutas cambiadas por ti. Igualmente, usar estos métodos te dará mensajes
de error descriptivos si hay un enlace roto.

.. highlight:: jinja

La indentación en las plantillas debería manejarse de la siguiente manera::

    {% if indenting %}
      <p>Así es que se hace</p>
    {% endif %}


.. index:: playdoh

Playdoh
^^^^^^^

Las nuevas aplicaciones Web deberían estar basadas en Playdoh_ y las
existentes deberían seguir el mismo espíritu de Playdoh_. Playdoh_
reune lecciones que varios proyectos hechos en Django en Mozilla han
aprendido y los envuelve en una plantilla para tus proyectos.

En el futuro, la mayor parte de los componentes de Playdoh_ serán
movidos a librerías separadas de manera que esas características no
se pierdan.

.. _Playdoh: https://github.com/mozilla/playdoh

.. index:: code;javascript coding style

Javascript
----------

Lee :ref:`js-style`.

.. index:: code;html5 coding style

HTML
----

* Usa HTML5
* Asegúrate de que tu código valida
* No coloques CSS o JS en el HTML
* Se semántico
* Usa comillas dobles para los atributos::

      <a href="#">Bueno</a>
      <a href='#'>Menos bueno</a>

