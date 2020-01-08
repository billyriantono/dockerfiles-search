FROM debian:latest

ENV S6_RELEASE 1.21.4.0

#Installs S6 overlay 
ADD https://github.com/just-containers/s6-overlay/releases/download/v$S6_RELEASE/s6-overlay-amd64.tar.gz /tmp/
RUN tar xzf /tmp/s6-overlay-amd64.tar.gz -C /

#Installs a few useless apps 
RUN apt-get update \
&& apt-get install cowsay fortune -y


COPY install.sh /etc/cont-init.d/
RUN chmod u+x /etc/cont-init.d/install.sh

ENTRYPOINT ["/init"]

