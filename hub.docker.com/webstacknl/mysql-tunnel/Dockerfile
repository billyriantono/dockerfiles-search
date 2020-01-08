FROM debian:stretch-slim
MAINTAINER Robbert van Mourik, robbert@webstack.nl

RUN apt-get update -y \
 && apt-get upgrade -y

RUN apt-get install -y ssh

COPY ./docker-entrypoint.sh /bin/docker-entrypoint.sh

RUN chmod +x /bin/docker-entrypoint.sh

ENTRYPOINT ["/bin/docker-entrypoint.sh"]

EXPOSE 3306 3306
