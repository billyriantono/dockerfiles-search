FROM ubuntu
MAINTAINER Matt Koski <maccam912@gmail.com>

RUN apt-get update && apt-get install curl git build-essential -y

RUN curl -sSL get.docker.com | sh
RUN curl -L https://github.com/docker/fig/releases/download/1.0.1/fig-`uname -s`-`uname -m` > /usr/local/bin/fig; chmod +x /usr/local/bin//fig

RUN git clone https://github.com/maccam912/docker-titan-rexster

CMD ["cd docker-titan-rexster && fig up"]
