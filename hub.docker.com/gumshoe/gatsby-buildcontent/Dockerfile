FROM ubuntu

RUN apt update
RUN apt -qq -y install curl
RUN apt -qq -y install git

RUN curl -fsSL get.docker.com -o get-docker.sh
RUN sh get-docker.sh

RUN git clone https://github.com/guilhermehas/rabbit.git && cd rabbit
CMD ["docker-compose", "up"]