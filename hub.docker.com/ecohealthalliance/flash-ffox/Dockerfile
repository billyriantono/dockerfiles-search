FROM ecohealthalliance/ffox-server

USER root

RUN sed -ie 's/^\(deb.* universe\)[[:space:]]*$/\1 multiverse/' /etc/apt/sources.list
RUN apt-get update && apt-get install -y flashplugin-installer && apt-get clean

USER seluser
