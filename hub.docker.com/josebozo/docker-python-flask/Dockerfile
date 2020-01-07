from ubuntu:16.04

MAINTAINER Jose Bozo <josebozo@hotmai.com>

RUN apt-get update && apt-get install -y \
    python-pip python-dev
RUN pip install flask

# Limpiar al terminar.
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*


