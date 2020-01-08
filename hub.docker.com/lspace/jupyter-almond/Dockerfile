FROM 	jupyter/minimal-notebook

LABEL 	maintainer="Thijs Broersen"

USER 	root

RUN 	apt-get update && apt-get upgrade -y

RUN 	apt-get install gnupg2 curl openjdk-8-jdk -y && \
        curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - && \
        echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list && \
        apt-get update && apt-get install yarn -y

RUN 	apt-get clean && rm -rf /var/lib/apt/lists/*

RUN     sh -c '(echo "#!/usr/bin/env sh" && curl -L https://github.com/lihaoyi/Ammonite/releases/download/1.6.3/2.12-1.6.3) > /usr/local/bin/amm && chmod +x /usr/local/bin/amm'

USER 	$NB_UID

RUN 	pip install --upgrade pip && \
        conda update -n base conda && \
        conda install -c conda-forge jupyterlab 
#	conda install -c conda-forge ipyleaflet

RUN 	curl -L -o coursier https://git.io/coursier && \
        chmod +x coursier && \
        ./coursier --help && \
        SCALA_VERSION=2.12.8 ALMOND_VERSION=0.3.0 && \
        ./coursier bootstrap \
        -r jitpack \
        -i user -I user:sh.almond:scala-kernel-api_$SCALA_VERSION:$ALMOND_VERSION \
        sh.almond:scala-kernel_$SCALA_VERSION:$ALMOND_VERSION \
        --sources --default=true \
        -o almond && \
        ./almond --install && \
        rm -f almond && \
        SCALA_VERSION=2.11.12 ALMOND_VERSION=0.3.0 && \
        ./coursier bootstrap \
        -r jitpack \
        -i user -I user:sh.almond:scala-kernel-api_$SCALA_VERSION:$ALMOND_VERSION \
        sh.almond:scala-kernel_$SCALA_VERSION:$ALMOND_VERSION \
        --sources --default=true \
        -o almond-scala-2.11 && \
        ./almond-scala-2.11 --install --id scala211 --display-name "Scala (2.11)" && \
        rm -f almond-scala-2.11

RUN 	jupyter labextension install @jupyter-widgets/jupyterlab-manager --no-build && \
        jupyter labextension install @jupyterlab/hub-extension --no-build && \
        jupyter labextension install @jupyterlab/theme-dark-extension --no-build && \
        jupyter labextension install @jupyterlab/theme-light-extension --no-build && \
        jupyter labextension install @oriolmirosa/jupyterlab_materialdarker --no-build && \
        jupyter labextension install @jupyterlab/git --no-build && \
        jupyter labextension install @jupyterlab/plotly-extension --no-build && \
        jupyter labextension install @jupyterlab/toc --no-build && \
        jupyter labextension install @jupyterlab/vega3-extension --no-build && \
        jupyter labextension install jupyterlab-drawio --no-build && \
#        jupyter labextension install jupyter-leaflet --no-build && \
#        jupyter labextension install jupyterlab_voyager --no-build && \
        export NODE_OPTIONS=--max-old-space-size=16000 && jupyter lab build
