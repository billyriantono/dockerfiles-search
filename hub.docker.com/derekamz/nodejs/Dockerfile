FROM derekamz/debian:stretch
ENV NODE_VER=6.11.3
ENV PATH $PATH:/nodejs/bin

RUN apt-get update -y && apt-get install --no-install-recommends -y -q curl python build-essential git ca-certificates
RUN curl -SLO https://nodejs.org/dist/v${NODE_VER}/node-v${NODE_VER}-linux-x64.tar.gz \
    && tar xvzf node-v${NODE_VER}-linux-x64.tar.gz -C /usr/local --strip-components=1 \
    && rm node-v${NODE_VER}-linux-x64.tar.gz \
    && npm install -g cnpm --registry=https://registry.npm.taobao.org

CMD ["node"]
