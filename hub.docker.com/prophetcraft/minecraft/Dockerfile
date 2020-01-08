FROM store/oracle/serverjre:8
MAINTAINER prophetcraft

RUN mkdir /minecraft
WORKDIR /minecraft
COPY run.sh /minecraft/

VOLUME /minecraft
EXPOSE 25565:25565

CMD sh /minecraft/run.sh
