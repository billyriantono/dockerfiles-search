FROM opensuse/leap:latest

MAINTAINER lemmy04 <Mathias.Homann@openSUSE.org>

RUN zypper install -y -l --recommends mono-core mono-extras unzip curl

LABEL version=1.1.6887.19595 Description="For running an AI module for corrade bots" Vendor="lemmy04"

ADD [ "http://corrade.grimore.org/download/release/corrade-ai/Corrade-AI-1.1.6887.19595.zip", "/tmp/corradeAI.zip" ]
ADD [ "./run.sh", "/usr/src/app/CorradeAI/run.sh" ]
ADD [ "Configuration.xml", "/usr/src/app/CorradeAI/Configuration.xml" ]

RUN mkdir -p /usr/src/app/CorradeAI
RUN unzip -d /usr/src/app/CorradeAI /tmp/corradeAI.zip 


# CorradeAI Port
EXPOSE 1443

WORKDIR /usr/src/app/CorradeAI
CMD /usr/src/app/CorradeAI/run.sh

