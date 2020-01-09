FROM centos 

MAINTAINER Aaron Wong

ENV APPHOME=/usr/src/bnserver
ENV SRC=files

COPY $SRC $APPHOME

WORKDIR $APPHOME

CMD [ "bash", "run_server.sh", "-p", "1234", "start"]
