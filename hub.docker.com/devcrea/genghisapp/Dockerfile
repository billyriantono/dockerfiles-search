FROM ruby:slim
MAINTAINER "VAILLANT Jérémy" <vaillant.jeremy@dev-crea.com>

RUN apt-get update && apt-get install -y bison gcc make autoconf

RUN gem install --no-ri --no-rdoc bson_ext:1.9.2 genghisapp

CMD genghisapp --no-launch --foreground --port=5000 --servers ${DB_PORT_27017_TCP_ADDR}:${DB_PORT_27017_TCP_PORT}/${DB_NAME}
