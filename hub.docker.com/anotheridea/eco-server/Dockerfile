FROM debian:stretch-slim

### Install Dependencies (Mono, unzip, ...)
### TODO: Move to base image
ADD install_deps.sh / 
RUN /install_deps.sh 

### Basic settings for Eco Server
WORKDIR /srv/eco-server
EXPOSE 2999/udp 2999 3000/udp 3001

CMD ["/srv/eco-server/start.sh"]

ADD SHA256SUMS ./

ENV ECO_VERSION="0.7.4.6-beta"
LABEL eco.version=${ECO_VERSION}

### Install Eco Server
ADD install.sh ./
ADD start.sh ./

RUN /srv/eco-server/install.sh
