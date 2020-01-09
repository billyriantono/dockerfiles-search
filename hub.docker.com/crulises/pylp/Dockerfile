FROM ubuntu:xenial
MAINTAINER Ulises C. Ramirez - ulir19[at]gmail[dot]com

# Variables de Entorno
ENV PATH="/home/pylp/herramientas/:${PATH}"

# Creación de volúmenes montables para el contenedor
VOLUME ["/home/pylp/codigo", "/home/pylp/herramientas"]

# Actualizacion de repositorios
RUN apt-get update

# Instalacion de las herramientas necesarias
RUN apt-get install -y g++ libopenmpi-dev ghc swi-prolog

RUN apt-get clean && \
	apt-get autoclean && \
	apt-get autoremove

# Agrega usuario pylp
RUN useradd --shell /bin/bash pylp

# Agrego script para la compilación/interpretación
COPY ./pylp_ci /home/pylp/herramientas/pylp_ci
RUN chmod +x /home/pylp/herramientas/pylp_ci
RUN chown pylp:pylp /home/pylp/herramientas/pylp_ci

# Iniciar como usuario pylp, no root
USER pylp

WORKDIR /home/pylp/codigo

CMD ["/bin/bash"]
