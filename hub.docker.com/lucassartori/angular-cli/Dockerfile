FROM node
MAINTAINER Lucas Antonio Ramos Sartori <faltou.criatividade0@gmail.com>

ENV TZ=America/Sao_Paulo
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

RUN apt-get update && apt-get -y upgrade
RUN apt-get install sudo nano
RUN apt-get install build-essential -y
RUN apt-get install curl -y
RUN apt-get install yarn -y
RUN apt-get install apt-utils -y

RUN npm i -g typescript
RUN npm i -g json-server
RUN npm i -g @angular/cli


# Expose ports.
EXPOSE 4200
EXPOSE 9000

CMD /bin/bash
