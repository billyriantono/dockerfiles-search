FROM bigzeta/ci_python3_node:1.2.3

ENV DOCKERIZE_VERSION v0.6.1

RUN sudo /bin/bash -c 'sudo curl -L https://github.com/docker/compose/releases/download/1.17.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose' && \
    sudo chmod +x /usr/local/bin/docker-compose

RUN cd /tmp && \
    wget https://github.com/jwilder/dockerize/releases/download/${DOCKERIZE_VERSION}/dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz && \
    sudo tar -C /usr/local/bin -xzvf dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz && \
    rm dockerize-linux-amd64-${DOCKERIZE_VERSION}.tar.gz


