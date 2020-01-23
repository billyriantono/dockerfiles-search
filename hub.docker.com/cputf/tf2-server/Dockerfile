FROM ubuntu:18.04
LABEL maintainer="Jonathan Penton <jonathan@penton.site>"

RUN dpkg --add-architecture i386
RUN apt-get update -y && apt-get upgrade -y && apt-get install -y lib32z1 lib32ncurses5 libbz2-1.0:i386 lib32gcc1 lib32stdc++6 wget gdb libcurl3-gnutls:i386

ENV SERVER /app
WORKDIR $SERVER

RUN wget -O - http://media.steampowered.com/installer/steamcmd_linux.tar.gz | tar -C $SERVER -xvz

COPY tf2_ds.txt ./
RUN ./steamcmd.sh +runscript tf2_ds.txt

RUN mkdir /root/.steam/sdk32
RUN ln -s /app/linux32/steamclient.so /root/.steam/sdk32/steamclient.so
