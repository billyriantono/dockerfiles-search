# Ionic dans un container
#
# VERSION               0.0.1
#

FROM     fwed/node-js
MAINTAINER Gallyoko "yogallyko@gmail.com"

# Definition des constantes
ENV login_ssh="ionic"
ENV password_ssh="ionic"

# Mise a jour des depots
RUN (apt-get update && apt-get upgrade -y -q && apt-get -y -q autoclean && apt-get -y -q autoremove)

# ionic / cordova
RUN npm install -g ionic cordova

# Ajout utilisateur "${login_ssh}"
RUN adduser --quiet --disabled-password --shell /bin/bash --home /home/${login_ssh} --gecos "User" ${login_ssh}

# Modification du mot de passe pour "${login_ssh}"
RUN echo "${login_ssh}:${password_ssh}" | chpasswd

EXPOSE 22 35729 53703 8100
