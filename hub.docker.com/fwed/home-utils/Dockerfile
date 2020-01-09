# HomeUtils dans un container
#
# VERSION               0.0.1
#

FROM     fwed/nodejs-base-project
MAINTAINER Fwedoz "fwedoz@gmail.com"

# Definition des constantes
ENV login_ssh="docker"

# Mise a jour des depots
RUN (apt-get update && apt-get upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)

# Installation des paquets necessaires
RUN apt-get install -y -q git

# Telechargement et installation de HomeUtils
COPY install.sh /root/install.sh
RUN chmod -f 755 /root/install.sh
RUN sh /root/install.sh

EXPOSE 22 8100 35729

# Modification de services.sh
RUN rm -f /root/services.sh
COPY services.sh /root/services.sh
RUN chmod -f 755 /root/services.sh

VOLUME ["/home/${login_ssh}"]
