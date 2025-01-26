.. _known_bugs:

#######################
Lista de Bugs Conocidos
#######################

A continuación, puede encontrar una lista con formato JSON de algunos de
los errors conocidos relevantes en el compilador Solidity. El archivo se
encuentra en el `repositorio de Github <https://github.com/ethereum/solidity/block/develop/docs/bugs.json>`_. 
La lista se extiende hasta la versión 0.3.0; los errors que se sabe solo 
están presentes en versiones anteriores no aparecen en la lista.

Hay otro archivo llamado `bugs_by_version.json <https://github.com/ethereum/solidity/blob/develop/docs/bugs_by_version.json>`_, que se puede utilizar para comprobar qué errores afectan a una versión específica del compilador.

Herramientas para la verificación del código fuente de un contrato, y otras herramientas que interactúen con contratos, deben consultar esta lista de acuerdo a los siguientes criterios:

- Se puede sospechar levemente si un contrato fue compilado con una versión nightly del compilador, en vez de un versión publicada.
  Esta lista no realiza un seguimiento de las versiones que no han sido publicadas o versiones nightly.
- También se puede sospechar levemente si un contrato se compiló con una versión que no era la más reciente en el momento de la creación del contrato.
  Para los contratos creados a partir de otros contratos, se debe seguir la cadena de creación hasta una transacción, y usar la fecha de esa transacción como fecha de creación.
- Se puede sospechar altamente si un contrato se compiló con un compilador que contiene un bug conocido y el contrato se creó en un momento en el que ya se había lanzado una versión más reciente del compilador que ya contenía una corrección.

El archivo JSON de bugs conocidos, que se encuentra a continuación, es una matriz de objetos, uno por cada error, con las siguientes claves:

uid
    Identificador único dado al error en forma de ``SOL-<año>-<número>``. Es posible que existan varias entradas con el mismo uid. Esto significa que varios rangos de versiones se ven afectados por el mismo error.
name
    Nombre único que se le da al bug.
summary
    Una breve descripción del bug.
description
    Una descripción detallada del bug.
link
    URL del sitio web con información detallada. Opcional.
introduced
    La primera versión del compilador publicada que contenía el bug. Opcional.
fixed
    La primera versión del compilador publicada que ya no contenía el bug.
publish
    La fecha en la que el bug se hizo público. Opcional.
severity
    Gravedad del bug: muy baja, baja, media, alta.
    Se toma en cuenta la detectabilidad en los tests del contrato, probabilidad de ocurrencia y daños potenciales por exploits.
conditions
    Condiciones que deben cumplirse para desencadenar el bug.
    Se pueden utilizar las siguientes claves:
    ``optimizer``, Valor de tipo boolean, lo que significa que el optimizador debe ser encendido para habilitar el bug.
    ``evmVersion``, un string que indica qué tipo de configuración del compilador de la versión de EVM desencadena el bug.
    El string puede contener operadores de comparación.
    Por ejemplo, ``">=constantinople"`` significa que el bug está presente cuando la versión de EVM se establece en "constantinople" o posterior.
    Si no hay condiciones, se debe suponer que el bug aún siga presente.
check
    This field contains different checks that report whether the smart contract
    contains the bug or not. The first type of check are JavaScript regular
    expressions that are to be matched against the source code ("source-regex")
    if the bug is present.  If there is no match, then the bug is very likely
    not present. If there is a match, the bug might be present.  For improved
    accuracy, the checks should be applied to the source code after stripping
    comments.
    The second type of check are patterns to be checked on the compact AST of
    the Solidity program ("ast-compact-json-path"). The specified search query
    is a `JsonPath <https://github.com/json-path/JsonPath>`_ expression.
    If at least one path of the Solidity AST matches the query, the bug is
    likely present.

.. literalinclude:: bugs.json
   :language: js
