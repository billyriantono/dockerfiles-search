FROM node:latest
MAINTAINER Raul Perez <repejota@gmail.com>

RUN apt-get -y update
RUN npm install gitbook -g

COPY ./run.sh /run.sh

VOLUME /src
VOLUME /output

WORKDIR /src
CMD ["/run.sh"]
