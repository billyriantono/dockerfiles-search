FROM neurodebian:latest

RUN apt-get update \
 && export DEBIAN_FRONTEND=noninteractive \
 && apt-get install -y ants
WORKDIR /usr/lib/ants