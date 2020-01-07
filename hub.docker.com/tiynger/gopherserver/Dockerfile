FROM ubuntu

MAINTAINER mail@martenkante.de

ENV SERVER_NAME localhost

RUN apt-get update

RUN apt-get install pygopherd -y

ADD run.sh /

RUN chmod +x run.sh 

VOLUME /var/gopher

EXPOSE 70

CMD ["./run.sh"]
