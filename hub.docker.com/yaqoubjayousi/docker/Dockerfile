
FROM node:8

RUN echo "deb http://httpredir.debian.org/debian jessie-backports main" >> /etc/apt/sources.list

RUN dpkg --add-architecture i386

RUN apt-get -y install libstdc++6

RUN wget -nc https://dl.winehq.org/wine-builds/Release.key

RUN apt-key add Release.key

RUN apt-get update && apt-get -y install apt-transport-https curl

RUN echo "deb https://dl.winehq.org/wine-builds/debian/ jessie main" | tee -a /etc/apt/sources.list

RUN apt-get update 

RUN apt-get -y install --install-recommends winehq-stable