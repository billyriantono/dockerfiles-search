FROM ubuntu:14.04

RUN apt-get update && apt-get -y install wget
RUN wget https://raw.githubusercontent.com/dokku/dokku/v0.6.5/bootstrap.sh

EXPOSE 22
EXPOSE 80
EXPOSE 443

CMD ["bash", "DOKKU_TAG=v0.6.5 bash bootstrap.sh"]
