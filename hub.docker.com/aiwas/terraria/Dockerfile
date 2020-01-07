FROM frolvlad/alpine-glibc
MAINTAINER Kuwano Miyako <aiwas@arg.vc>

ARG TERRARIA_VERSION

RUN apk update && apk upgrade && apk add wget unzip screen
RUN adduser -D -u 1001 terraria
RUN mkdir -p /opt/Terraria && chown terraria:terraria /opt/Terraria
WORKDIR /opt/Terraria
USER terraria

RUN wget -nv -O server.zip http://terraria.org/server/terraria-server-${TERRARIA_VERSION}.zip
RUN unzip -q server.zip ${TERRARIA_VERSION}/Linux/* && mv ${TERRARIA_VERSION}/Linux/* . && rm -rf ${TERRARIA_VERSION}/ && chmod +x TerrariaServer.bin.x86_64

EXPOSE 7777
CMD ["/usr/bin/screen", "-D", "-m", "-A", "-S", "terraria", "/opt/Terraria/TerrariaServer.bin.x86_64", "-config", "serverconfig.txt"]
