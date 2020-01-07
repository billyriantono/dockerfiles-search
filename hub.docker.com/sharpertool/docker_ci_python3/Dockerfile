FROM sharpertool/ci_python3_node:1.4.1

ENV DOCKERIZE_VERSION v0.6.1
ENV COMPOSE_VERSION 1.23.2

RUN sudo pip install docker-compose==${COMPOSE_VERSION}

RUN cd /tmp && \
    wget https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz && \
    sudo tar -C /usr/local/bin -xzvf dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz && \
    rm dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz


