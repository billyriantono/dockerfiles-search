# vi:syntax=dockerfile

FROM microsoft/dotnet:2.1-sdk-stretch

ENV NODE_VERSION 8.12.0

RUN curl -sSLo node.tar.gz https://nodejs.org/dist/v${NODE_VERSION}/node-v${NODE_VERSION}-linux-x64.tar.gz \
    && tar -xzf node.tar.gz \
    && rm node.tar.gz \
    && mv node-v8.12.0-linux-x64 /usr/share/node \
    && ln -s /usr/share/node/bin/node /usr/bin/node \
    && ln -s /usr/share/node/bin/npm /usr/bin/npm
