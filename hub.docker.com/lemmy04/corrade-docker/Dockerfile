FROM opensuse/leap:latest

MAINTAINER lemmy04 <Mathias.Homann@openSUSE.org>

RUN zypper install -y -l --recommends mono-core mono-extras unzip curl

LABEL version=10.3.7119.25375 Description="For running Second Life and OpenSim automated agents based on the Corrade scripted agent system" Vendor="ICON Metaverse"

ADD [ "http://corrade.grimore.org/download/release/corrade/Corrade-10.3.7119.25375.zip", "/tmp/corrade.zip" ]
ADD [ "./run.sh", "/usr/src/app/Corrade/run.sh" ]

RUN mkdir -p /usr/src/app/Corrade
RUN unzip -d /usr/src/app/Corrade /tmp/corrade.zip 


# MQTT Port
EXPOSE 1883

# HTTP Port
EXPOSE 8080

# TCP Port
EXPOSE 8085

# Websockets Port
EXPOSE 8088

# Nucleus Port
EXPOSE 54377

HEALTHCHECK --interval=5s --timeout=3s --retries=3 \
      CMD curl -f http://localhost:54377 || exit 1
      
WORKDIR /usr/src/app/Corrade
CMD /usr/src/app/Corrade/run.sh

