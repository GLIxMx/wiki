Bienvenid@
==========
Ésta es nuestra wiki.

Procuraremos mantenerla bien chida y llena de información relevante al FOSS.

Instrucciones
=============

.. code:: bash

    # clona el repositorio
    mkdir -p ~/src/glix
    cd ~/src/glix
    git clone ssh://<usuario>@glix.org.mx/srv/git/repos/glix-wiki.git wiki

    # si ya habías clonado el repo, entonces, haz pull primero:
    cd ~/src/glix/wiki
    git pull origin master

    # haz algunos cambios
    ## vim algo_chido.rst

    ## commit
    ## git commit -m 'algo chido: es mi borrador inicial' algo_chido.rst

    ## push (si es la primera vez, usa -u)
    ## git push -u origin master

    ## push (de la segunda para adelante)
    ## git push

Puedes usar la interfaz web en: http://wiki.glix.org.mx para ver lo que has publicado.

En caso de que quieras usar gollum localmente, para editar la wiki, solamente necesitas hacer lo siguiente:

.. code:: bash

    #!/usr/bin/env bash

    # crear un directorio
    mkdir -p glix-wiki/log
    cd glix-wiki

    # obtener los archivos necesarios
    wget -c --no-check-certificate http://wiki.glix.org.mx/Home/glix-wiki.tar.gz

    # descomprimirla
    tar -xaf glix-wiki.tar.xz

    # generar la configuración de thin
    cat << EOF > config/thin.conf
    ---
    address: 127.0.0.1
    chdir: ${PWD}
    daemonize: false
    environment: development
    log: log/thin.log
    pid: /run/wiki.glix.org.mx.pid
    port: 3000
    require: []
    threaded: true
    timeout: 30
    wait: 30

    EOF

    # instalar las dependencias
    bundle

    # correrlo
    bundle exec thin -C config/thin.conf start

    # accesarlo en http://localhost:3000/

Recuerda, tras editar los archivos, necesitas hacer push al repo de git remoto. No porque veas los cambios en tu interfaz local
quiere decir que están en la interfaz remota (Internet).

Feliz edición de la wiki!
