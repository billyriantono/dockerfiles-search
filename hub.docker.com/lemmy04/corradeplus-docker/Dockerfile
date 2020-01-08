FROM opensuse/leap:latest

MAINTAINER lemmy04 <Mathias.Homann@openSUSE.org>

RUN zypper install -y -l --recommends mono-core mono-extras unzip curl

LABEL version=10.3.7119.25375 Description="A container to run Corrade and the Corrade AI module, for chat bots in Second Life and compatible grids" Vendor="lemmy04"

ADD [ "http://corrade.grimore.org/download/release/corrade/Corrade-10.3.7119.25375.zip", "/tmp/corrade.zip" ]
ADD [ "http://corrade.grimore.org/download/release/corrade-ai/Corrade-AI-1.1.6887.19595.zip", "/tmp/corradeAI.zip" ]

ADD [ "Configuration.xml", "/usr/src/app/CorradeAI/Configuration.xml" ]
ADD [ "./run.sh", "/usr/src/app/Corrade/run.sh" ]

RUN mkdir -p /usr/src/app/Corrade
RUN unzip -d /usr/src/app/Corrade /tmp/corrade.zip 
RUN mkdir -p /usr/src/app/CorradeAI
RUN unzip -d /usr/src/app/CorradeAI /tmp/corradeAI.zip 


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

