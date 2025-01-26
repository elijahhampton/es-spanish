.. index:: ! installing

.. _installing-solidity:

####################################
Instalando el compilador de Solidity
####################################

Versionado
==========

Solidity versions follow `Semantic Versioning <https://semver.org>`_. In
addition, patch-level releases with major release 0 (i.e. 0.x.y) will not
contain breaking changes. That means code that compiles with version 0.x.y
can be expected to compile with 0.x.z where z > y.

In addition to releases, we provide **nightly development builds** to make
it easy for developers to try out upcoming features and
provide early feedback. Note, however, that while the nightly builds are usually
very stable, they contain bleeding-edge code from the development branch and are
not guaranteed to be always working. Despite our best efforts, they might
contain undocumented and/or broken changes that will not become a part of an
actual release. They are not meant for production use.

Al desplegar contratos, debería usar el último lanzamiento de Solidity. Esto es 
porque regularmente se introducen cambios con rupturas, funcionalidades nuevas y 
correcciones de errores. Actualmente usamos un número de versión 0.x 
`para indicar el rápido ritmo de cambio <https://semver.org/lang/es/#spec-item-4>`_.

Remix
=====

*Recomendamos Remix para pequeños contratos y para aprender Solidity rápidamente.*

`Access Remix online <https://remix.ethereum.org/>`_, you do not need to install anything.
If you want to use it without connection to the Internet, go to
https://github.com/ethereum/remix-live/tree/gh-pages#readme and follow the instructions on that page.
Remix is also a convenient option for testing nightly builds
without installing multiple Solidity versions.

Further options on this page detail installing command-line Solidity compiler software
on your computer. Choose a command-line compiler if you are working on a larger contract
or if you require more compilation options.

.. _solcjs:

npm / Node.js
=============

Use ``npm`` para instalar ``solcjs``, un compilador de Solidity, de una manera portable 
y sencilla. El programa `solcjs` tiene menos funcionalidades que el resto de maneras de 
compilar detalladas más abajo en esta página. La documentación del 
:ref:`compilador de línea de comandos` asume que está usando el compilador con funcionalidad 
completa, ``solc``. El uso de ``solcjs`` está documentado dentro de su propio
`repositorio <https://github.com/ethereum/solc-js>`_.

Note: The solc-js project is derived from the C++
`solc` by using Emscripten, which means that both use the same compiler source code.
`solc-js` can be used in JavaScript projects directly (such as Remix).
Please refer to the solc-js repository for instructions.

.. code-block:: bash

    npm install -g solc

.. Nota::

    The command-line executable is named ``solcjs``.

    The command-line options of ``solcjs`` are not compatible with ``solc`` and tools (such as ``geth``)
    expecting the behavior of ``solc`` will not work with ``solcjs``.

Docker
======

Docker images of Solidity builds are available using the ``solc`` image from the ``ethereum`` organization.
Use the ``stable`` tag for the latest released version, and ``nightly`` for potentially unstable changes in the ``develop`` branch.

The Docker image runs the compiler executable so that you can pass all compiler arguments to it.
For example, the command below pulls the stable version of the ``solc`` image (if you do not have it already),
and runs it in a new container, passing the ``--help`` argument.

.. code-block:: bash

    docker run ethereum/solc:stable --help

You can specify release build versions in the tag. For example:

.. code-block:: bash

    docker run ethereum/solc:stable --help

Note

Specific compiler versions are supported as the Docker image tag such as `ethereum/solc:0.8.23`. We will be passing the
`stable` tag here instead of specific version tag to ensure that users get the latest version by default and avoid the issue of
an out-of-date version.

To use the Docker image to compile Solidity files on the host machine, mount a
local folder for input and output, and specify the contract to compile. For example:

.. code-block:: bash

    docker run -v /local/path:/sources ethereum/solc:stable -o /sources/output --abi --bin /sources/Contract.sol

You can also use the standard JSON interface (which is recommended when using the compiler with tooling).
When using this interface, it is not necessary to mount any directories as long as the JSON input is
self-contained (i.e. it does not refer to any external files that would have to be
:ref:`loaded by the import callback <initial-vfs-content-standard-json-with-import-callback>`).

.. code-block:: bash

    docker run ethereum/solc:stable --standard-json < input.json > output.json

Paquetes de Linux
=================

Los binarios de Solidity están disponibles en
`solidity/releases <https://github.com/ethereum/solidity/releases>`_.

También tenemos PPAs para Ubuntu, puede obtener la versión estable más 
reciente usando los siguientes comandos:

.. code-block:: bash

    sudo add-apt-repository ppa:ethereum/ethereum
    sudo apt-get update
    sudo apt-get install solc

La versión nocturna puede ser instalada usando estos comandos:

.. code-block:: bash

    sudo add-apt-repository ppa:ethereum/ethereum
    sudo add-apt-repository ppa:ethereum/ethereum-dev
    sudo apt-get update
    sudo apt-get install solc

Furthermore, some Linux distributions provide their own packages. These packages are not directly
maintained by us but usually kept up-to-date by the respective package maintainers.

For example, Arch Linux has packages for the latest development version as AUR packages: `solidity <https://aur.archlinux.org/packages/solidity>`_
and `solidity-bin <https://aur.archlinux.org/packages/solidity-bin>`_.

.. note::

    Please be aware that `AUR <https://wiki.archlinux.org/title/Arch_User_Repository>`_ packages
    are user-produced content and unofficial packages. Exercise caution when using them.

También hay un `paquete para snap <https://snapcraft.io/solc>`_, 
sin embargo actualmente **no se le da mantenimiento**. Se puede instalar en todas las
`distros de Linux respaldadas <https://snapcraft.io/docs/core/install>`_. Para instalar
la última versión estable de solc:

.. code-block:: bash

    sudo snap install solc

Si usted quiere ayudar a probar la última versión de desarrollo de Solidity 
con los cambios más recientes, por favor utilice el siguiente comando:

.. code-block:: bash

    sudo snap install solc --edge

.. Nota::

    El snap de ``solc`` usa confinamiento estricto. Este es el modo más seguro para paquetes
    de snap pero tiene sus limitaciones, como por ejemplo, el solo acceder a los archivos en sus
    directorios ``/home`` y ``/media``.
    Para más información, vaya a `Demystifying Snap Confinement <https://snapcraft.io/blog/demystifying-snap-confinement>`_.


Paquetes para macOs
===================

Distribuimos el compilador de Solidity a través de Homebrew
como una versión build-from-source. Los binarios pre-compilados
no son respaldados actualmente.

.. code-block:: bash

    brew update
    brew upgrade
    brew tap ethereum/ethereum
    brew install solidity

Para instalar la versión 0.4.x / 0.5.x más reciente de Solidity también puede usar 
``brew install solidity@4`` y ``brew install solidity@5``, respectivamente.

Si necesita una versión específica de Solidity puede instalar una 
fórmula de Homebrew directamente desde Github.

View
`solidity.rb commits on GitHub <https://github.com/ethereum/homebrew-ethereum/commits/master/solidity.rb>`_.

Copie el commit hash de la versión que quiere y haga check out en su máquina.

.. code-block:: bash

    git clone https://github.com/ethereum/homebrew-ethereum.git
    cd homebrew-ethereum
    git checkout <el-hash-va-aquí>

Instalar usando ``brew``:

.. code-block:: bash

    brew unlink solidity
    # ej. para instalar 0.4.8
    brew install solidity.rb

Binarios estáticos
==================

Mantenemos un repositorio con todos los binarios estáticos y versiones actuales del compilador 
para todas las plataformas respaldadas en `solc-bin`_. En esta locación también puede encontrar
las compilaciones nocturnas.

Este repositorio no es solamente una manera fácil y rápida para que los usuarios finales puedan
obtener los archivos binarios listos para usarse; también está pensado para ser amigable para
herramientas de terceros:

- The content is mirrored to https://binaries.soliditylang.org where it can be easily downloaded over
  HTTPS without any authentication, rate limiting or the need to use git.
- Content is served with correct `Content-Type` headers and lenient CORS configuration so that it
  can be directly loaded by tools running in the browser.
- Binaries do not require installation or unpacking (exception for older Windows builds
  bundled with necessary DLLs).
- We strive for a high level of backward-compatibility. Files, once added, are not removed or moved
  without providing a symlink/redirect at the old location. They are also never modified
  in place and should always match the original checksum. The only exception would be broken or
  unusable files with the potential to cause more harm than good if left as is.
- Files are served over both HTTP and HTTPS. As long as you obtain the file list in a secure way
  (via git, HTTPS, IPFS or just have it cached locally) and verify hashes of the binaries
  after downloading them, you do not have to use HTTPS for the binaries themselves.

The same binaries are in most cases available on the `Solidity release page on GitHub`_. The
difference is that we do not generally update old releases on the GitHub release page. This means
that we do not rename them if the naming convention changes and we do not add builds for platforms
that were not supported at the time of release. This only happens in ``solc-bin``.

The ``solc-bin`` repository contains several top-level directories, each representing a single platform.
Each one includes a ``list.json`` file listing the available binaries. For example in
``emscripten-wasm32/list.json`` you will find the following information about version 0.7.4:

.. code-block:: json

    {
      "path": "solc-emscripten-wasm32-v0.7.4+commit.3f05b770.js",
      "version": "0.7.4",
      "build": "commit.3f05b770",
      "longVersion": "0.7.4+commit.3f05b770",
      "keccak256": "0x300330ecd127756b824aa13e843cb1f43c473cb22eaf3750d5fb9c99279af8c3",
      "sha256": "0x2b55ed5fec4d9625b6c7b3ab1abd2b7fb7dd2a9c68543bf0323db2c7e2d55af2",
      "urls": [
        "bzzr://16c5f09109c793db99fe35f037c6092b061bd39260ee7a677c8a97f18c955ab1",
        "dweb:/ipfs/QmTLs5MuLEWXQkths41HiACoXDiH8zxyqBHGFDRSzVE5CS"
      ]
    }

Esto significa que:

- Puede encontrar el binario en el mismo directorio bajo el nombre
  `solc-emscripten-wasm32-v0.7.4+commit.3f05b770.js <https://github.com/ethereum/solc-bin/blob/gh-pages/emscripten-wasm32/solc-emscripten-wasm32-v0.7.4+commit.3f05b770.js>`_.
  Note that the file might be a symlink, and you will need to resolve it yourself if you are not using
  git to download it or your file system does not support symlinks.
- The binary is also mirrored at https://binaries.soliditylang.org/emscripten-wasm32/solc-emscripten-wasm32-v0.7.4+commit.3f05b770.js.
  In this case git is not necessary and symlinks are resolved transparently, either by serving a copy
  of the file or returning a HTTP redirect.
- The file is also available on IPFS at `QmTLs5MuLEWXQkths41HiACoXDiH8zxyqBHGFDRSzVE5CS`_.
- The file might in future be available on Swarm at `16c5f09109c793db99fe35f037c6092b061bd39260ee7a677c8a97f18c955ab1`_.
- You can verify the integrity of the binary by comparing its keccak256 hash to
  ``0x300330ecd127756b824aa13e843cb1f43c473cb22eaf3750d5fb9c99279af8c3``.  The hash can be computed
  on the command-line using ``keccak256sum`` utility provided by `sha3sum`_ or `keccak256() function
  from ethereumjs-util`_ in JavaScript.
- You can also verify the integrity of the binary by comparing its sha256 hash to
  ``0x2b55ed5fec4d9625b6c7b3ab1abd2b7fb7dd2a9c68543bf0323db2c7e2d55af2``.

.. Advertencia::

   Debido a los fuertes requerimientos de compatibilidad con versiones anteriores, el repositorio 
   contiene algunos elementos descontinuados que debería evitar usar al crear herramientas nuevas: 
   
   - Use ``emscripten-wasm32/`` (o en su defecto ``emscripten-asmjs/``) en lugar de ``bin/`` si 
     quiere el mejor rendimiento. Hasta la versión 0.6.1 solo proveíamos binarios de asm.js.
     A partir de la versión 0.6.2 hicimos el cambio a `WebAssembly builds`_ que tiene mucho mejor 
     rendimiento. Hemos recompilado las versiones más antiguas para wasm pero los archivos originales 
     asm.js se mantienen en ``bin/``. Los nuevos tuvieron que ser puestos en un directorio separado 
     para evitar conflictos de nombramiento.
   - Use los directorios ``emscripten-asmjs/`` y ``emscripten-wasm32/`` en lugar de ``bin/`` y ``wasm/``
     si quiere estar seguro de si está descargando un binario de wasm o de asm.js. 
   - Use ``list.json`` en vez de ``list.js`` y ``list.txt``. El formato JSON contiene toda la 
     información de los binarios antiguos y más.
   - Use https://binaries.soliditylang.org en vez de https://solc-bin.ethereum.org. Para mantener 
     las cosas simples, movimos casi todo lo relacionado al compilador al nuevo dominio 
     ``soliditylang.org`` y esto también aplica para ``solc-bin``. Aunque recomendamos el nuevo 
     dominio, el antiguo sigue siendo mantenido y se garantiza que apunte a la misma locación.

.. Advertencia::

    Los binarios también están disponbiles en https://ethereum.github.io/solc-bin/ pero esta página
    dejó de ser actualizada justo después del lanzamiento de la versión 0.7.2, no va a recibir 
    nuevos releases ni compilaciones nocturnas para ninguna plataforma y no sirve la nueva estructura
    del directorio, incluyendo compilaciones no-emscripten.

    Si usted la está usando, por favor cambie a https://binaries.soliditylang.org, que es su reemplazo.
    Esto nos permite hacerle cambios al hosting subyacente de una manera transparente y minimizar
    disrupciones. Al contrario del dominio ``ethereum.github.io``, el cual no controlamos, 
    ``binaries.soliditylang.org`` está garantizado para funcionar y mantener la misma estructura de URLs 
    en el largo plazo.

.. _IPFS: https://ipfs.io
.. _Swarm: https://swarm-gateways.net/bzz:/swarm.eth
.. _solc-bin: https://github.com/ethereum/solc-bin/
.. _Solidity release page on GitHub: https://github.com/ethereum/solidity/releases
.. _sha3sum: https://github.com/maandree/sha3sum
.. _función keccak256() de ethereumjs-util: https://github.com/ethereumjs/ethereumjs-util/blob/master/docs/modules/_hash_.md#const-keccak256
.. _WebAssembly builds: https://emscripten.org/docs/compiling/WebAssembly.html
.. _QmTLs5MuLEWXQkths41HiACoXDiH8zxyqBHGFDRSzVE5CS: https://gateway.ipfs.io/ipfs/QmTLs5MuLEWXQkths41HiACoXDiH8zxyqBHGFDRSzVE5CS
.. _16c5f09109c793db99fe35f037c6092b061bd39260ee7a677c8a97f18c955ab1: https://swarm-gateways.net/bzz:/16c5f09109c793db99fe35f037c6092b061bd39260ee7a677c8a97f18c955ab1/

.. _compilando-del-codigo-fuente:

Building from Source
====================
Prerequisites - All Operating Systems
-------------------------------------

A continuación las dependencias para todas las compilaciones de Solidity:

+-----------------------------------+-------------------------------------------------------+
| Software                          | Notas                                                 |
+===================================+=======================================================+
| `CMake`_ (version 3.21.3+ on      | Cross-platform build file generator.                  |
| Windows, 3.13+ otherwise)         |                                                       |
+-----------------------------------+-------------------------------------------------------+
| `Boost`_ (version 1.77+ on        | C++ libraries.                                        |
| Windows, 1.65+ otherwise)         |                                                       |
+-----------------------------------+-------------------------------------------------------+
| `Git`_                            | Software de línea de comandos para obtener código     |
|                                   | fuente.                                               |
+-----------------------------------+-------------------------------------------------------+
| `z3`_ (versión 4.8+, Opcional)    | Para usar con SMT checker.                            |
| `z3`_ (version 4.8.16+, Opcional) | Para usar con SMT checker.                            |
+-----------------------------------+-------------------------------------------------------+
| `cvc4`_ (Opcional)                | Para usar con SMT checker.                            |
+-----------------------------------+-------------------------------------------------------+

.. _cvc4: https://cvc4.cs.stanford.edu/web/
.. _Git: https://git-scm.com/download
.. _Boost: https://www.boost.org
.. _CMake: https://cmake.org/download/
.. _z3: https://github.com/Z3Prover/z3

.. note::
    Solidity versions prior to 0.5.10 can fail to correctly link against Boost versions 1.70+.
    A possible workaround is to temporarily rename ``<Boost install path>/lib/cmake/Boost-1.70.0``
    prior to running the cmake command to configure Solidity.

    A partir de la versión 0.5.10, debería funcionar correctamente con las versiones de Boost 
    1.70+ sin necesidad de ajustes manuales.

.. Nota::
    La configuración de la compilación por defecto requiere una versión de Z3 específica (la última 
    en el momento que el código se actualizó por última vez). Los cambios que hay entre versiones de
    Z3 generalmente dan como resultado lanzamientos ligeramente distintos (pero válidos). Nuestras
    pruebas SMT no toman en cuenta estas diferencias y probablemente fallarán con una versión diferente 
    de la versión para la que fueron escritas. Esto no significa que una compilación que use una 
    versión diferente está dañada. Si usted pasa la opción ``-DSTRICT_Z3_VERSION=OFF`` a CMake, puede
    compilar con cualquier versión que satisfaga los requerimientos de la tabla de arriba. Si hace esto,
    sin embargo, recuerde pasar la opción ``--no-smt`` a ``scripts/tests.sh`` para saltar las pruebas SMT.


Versiones Mínimas del Compilador
==============================

.. Nota::
    De forma predeterminada, la compilación se realiza en *modo pedante*, lo que activa advertencias 
    adicionales y le indica al compilador para tratar todas las advertencias como errores. 
    Esto obliga a los desarrolladores a corregir las advertencias a medida que surgen, de modo que no 
    acumulen que se solucionen más tarde. 
    Si sólo le interesa crear una versión de lanzamiento y no desea modificar el código fuente 
    para tratar estas advertencias, puede pasar la opción ``-DPEDANTIC=OFF` a CMake para deshabilitar 
    este modo. No se recomienda hacerlo para uso general, pero puede ser necesario cuando se utiliza 
    una cadena de herramientas que estamos no probar o intentar crear una versión anterior con 
    herramientas más recientes. Si encuentra este tipo de advertencias, tenga en cuenta `reporting them 
    <https://github.com/ethereum/solidity/issues/new>`_.
    

Los siguientes compiladores de C++ y sus versiones mínimas pueden compilar el código de Solidity:

- `GCC <https://gcc.gnu.org>`_, versión 8+
- `Clang <https://clang.llvm.org/>`_, versión 7+
- `MSVC <https://visualstudio.microsoft.com/vs/>`_, versión 2019+

For macOS builds, ensure that you have the latest version of
`Xcode installed <https://developer.apple.com/xcode/resources/>`_.
This contains the `Clang C++ compiler <https://en.wikipedia.org/wiki/Clang>`_, the
`Xcode IDE <https://en.wikipedia.org/wiki/Xcode>`_ and other Apple development
tools that are required for building C++ applications on OS X.
If you are installing Xcode for the first time, or have just installed a new
version then you will need to agree to the license before you can do
command-line builds:

.. code-block:: bash

    sudo xcodebuild -license accept

Nuestro script de compilación para OS X usa el gestor de paquetes 
`Homebrew <https://brew.sh>`_ para instalar dependencias externas. 
Aquí puede ver cómo `desinstalar Homebrew
<https://docs.brew.sh/FAQ#how-do-i-uninstall-homebrew>`_, si necesita
empezar desde cero.

Prerrequisitos - Windows
-----------------------

Necesitará instalar las siguientes dependencias para compilar Solidity en Windows:

+-----------------------------------+-------------------------------------------------------+
| Software                          | Notas                                                 |
+===================================+=======================================================+
| `Visual Studio 2019 Build Tools`_ | Compilador de C++                                     |
+-----------------------------------+-------------------------------------------------------+
| `Visual Studio 2019`_  (Opcional) | Compilador de C++ y entorno de desarrollo             |
+-----------------------------------+-------------------------------------------------------+
| `Boost`_ (version 1.77+)          | C++ libraries.                                        |
+-----------------------------------+-------------------------------------------------------+

Si ya tiene un IDE y solo necesita instalar el compilador y las librerías, puede instalar
solamente Visual Studio 2019 Build Tools.

Visual Studio 2019 provee un IDE y el compilador y librerías necesarias.
Si usted todavía no cuenta con un IDE de su preferencia y desea programar en Solidity,
Visual Studio 2019 puede ser una opción para configurar todo de manera sencilla.

A continuación, una lista de componentes que deben ser instalados ya sea que use
Visual Studio 2019 o Visual Studio 2019 Build Tools.

* Visual Studio C++ core features
* VC++ 2019 v141 toolset (x86,x64)
* Windows Universal CRT SDK
* Windows 8.1 SDK
* C++/CLI support

.. _Visual Studio 2019: https://www.visualstudio.com/vs/
.. _Visual Studio 2019 Build Tools: https://visualstudio.microsoft.com/vs/older-downloads/#visual-studio-2019-and-other-products

Tenemos un script de soporte que puede usar para instalar todas las dependencias externas necesarias:

.. code-block:: bat

    scripts\install_deps.ps1

Esto instalará ``boost`` y ``cmake`` al subdirectorio ``deps``.

Clonar el repositorio
---------------------

Para clonar el código fuente ejecute el siguiente comando:

.. code-block:: bash

    git clone --recursive https://github.com/ethereum/solidity.git
    cd solidity

If you want to help develop Solidity,
you should fork Solidity and add your personal fork as a second remote:

.. code-block:: bash

    git remote add personal git@github.com:[username]/solidity.git

.. note::
    This method will result in a pre-release build leading to e.g. a flag
    being set in each bytecode produced by such a compiler.
    If you want to re-build a released Solidity compiler, then
    please use the source tarball on the GitHub release page:

    https://github.com/ethereum/solidity/releases/download/v0.X.Y/solidity_0.X.Y.tar.gz

    (not the "Source code" provided by GitHub).

Compilación por la línea de comandos
------------------------------------

**Asegúrese de instalar todas las dependencias externas (ver arriba) antes de compilar.**

El proyecto de Solidity utiliza CMake para configurar la compilación.
Se recomienda instalar `ccache`_ para acelerar el proceso si requiere compilar
en repetidas ocasiones.
CMake lo detectará automaticamente.
Compilar Solidity es bastante parecido en Linux, macOS y otras versiones de Unix:

.. _ccache: https://ccache.dev/

.. code-block:: bash

    mkdir build
    cd build
    cmake .. && make

En Linux y macOS es todavía más fácil, puede correr:

.. code-block:: bash

    #nota: esto instalará los binarios solc y soltest en usr/local/bin
    ./scripts/build.sh

.. Advertencia::

    Las compilaciones en BSD deberían funcionar, pero no han sido probadas por el equipo de Solidity.

Y para Windows:

.. code-block:: bash

    mkdir build
    cd build
    cmake -G "Visual Studio 16 2019" ..

En caso de querer usar la versión de boost instalada por ``scripts\install_deps.ps1``, deberá 
pasar adicionalmente las banderas ``-DBoost_DIR="deps\boost\lib\cmake\Boost-*"`` y 
``-DCMAKE_MSVC_RUNTIME_LIBRARY=MultiThreaded`` como argumentos cuando corra ``cmake``.

Esto debería crear un archivo **solidity.sln** en ese directorio. Al hacer doble click 
en ese archivo Visual Studio debería abrirse. Sugerimos compilar con la configuración 
**Release** pero todas las demás funcionan.

De manera alternativa, puede compilar en Windows desde la línea de comandos:

.. code-block:: bash

    cmake --build . --config Release

Opciones de CMake
=================

Para ver las opciones de Cmake disponibles solo corra ``cmake .. -LH``.

.. _smt_solvers_build:

SMT Solvers
-----------
Solidity can be built against SMT solvers and will do so by default if
they are found in the system. Each solver can be disabled by a ``cmake`` option.

*Nota: En algunos casos, esto también puede ser una solución alterna para compilaciones fallidas.*

En la carpeta donde compile puede deshabilitarlos, ya que están habilitados por defecto:

.. code-block:: bash

    # deshabilita solo el solver SMT para Z3
    cmake .. -DUSE_Z3=OFF

    # deshabilita solo el solver SMT para CVC4
    cmake .. -DUSE_CVC4=OFF

    # deshabilita los solvers para CVC4 y Z3
    cmake .. -DUSE_CVC4=OFF -DUSE_Z3=OFF

La Cadena de Versión en Detalle
===============================

La cadena de versión de Solidity contiene cuatro partes:

- el número de versión
- la etiqueta de pre-release, generalmente fijada en ``develop.YYYY.MM.DD`` o ``nightly.YYYY.MM.DD``
- commit en el formato ``commit.GITHASH``
- la plataforma, que contiene un número arbitrario de elementos, e incluye detalles sobre la plataforma y el compilador

Si hay modificaciones locales, el commit tendrá el sufijo de ``.mod``.

Estas partes se combinan según requerimientos de SemVer, donde la etiqueta de pre-release de Solidity equivale al 
pre-release de SemVer y el commit de Solidity y la plataforma combinados nos dan la metadata del compilado de SemVer.

Un ejemplo de release: ``0.4.8+commit.60cc1668.Emscripten.clang``.

Un ejemplo de pre-release: ``0.4.9-nightly.2017.1.17+commit.6ecb4aa3.Emscripten.clang``

Información Importante Sobre el Versionado
==========================================

Después de que se hace un lanzamiento, se aumenta el número de versión de parche, porque asumimos
que solo siguen cambios a nivel de parches. Cuando los cambios se fusionan, la versión debería ser
aumentada de acuerdo a SemVer y a la severidad del cambio. Finalmente, un lanzamiento siempre se hace 
con la versión de la compilación nocturna vigente, pero sin el especificador de ``prerelease``.

Ejemplo:

1. Se hace el release de la versión 0.4.0.
2. La compilación nocturna tiene una versión de 0.4.1 de ahora en adelante.
3. Se introducen cambios sin rupturas --> no hay cambio en la versión.
4. Se introduce un cambio con rupturas --> la versión se aumenta a 0.5.0.
5. Se hace el release de la versión 0.5.0.

This behavior works well with the  :ref:`version pragma <version_pragma>`.
