FROM cnpallares/docker-base

LABEL Carles Albert Pallares <carlesalbert.pallares@gmail.com>

ENV NODEJS_VERSION=9.2.1 \
    PATH=$PATH:/opt/node/bin

WORKDIR "/opt/node"

RUN apt-get update && apt-get install -y curl ca-certificates --no-install-recommends && \
    curl -sL https://nodejs.org/dist/v${NODEJS_VERSION}/node-v${NODEJS_VERSION}-linux-x64.tar.gz | tar xz --strip-components=1 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean