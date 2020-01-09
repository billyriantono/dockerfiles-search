FROM consol/ubuntu-xfce-vnc
MAINTAINER Tobias Schneck "tobias.schneck@consol.de"
ENV REFRESHED_AT 2017-04-10

## Install a gedit
USER 0
RUN apt-get update \
    && wget https://github.com/Tribler/tribler/releases/download/v7.0.1/tribler_7.0.1_all.deb \
    && DEBIAN_FRONTEND=noninteractive apt-get install -y ./tribler_7.0.1_all.deb
    
## switch back to default user
USER 1984
