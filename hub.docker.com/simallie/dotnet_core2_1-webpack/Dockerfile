# Docker image for .NET Core with webpack
FROM microsoft/dotnet:2.1-sdk

ENV NPM_CONFIG_LOGLEVEL info
ENV NODE_VERSION 8.11.2

RUN curl -SLO "https://nodejs.org/dist/v$NODE_VERSION/node-v$NODE_VERSION-linux-x64.tar.gz" \
    && tar -zxvf "node-v$NODE_VERSION-linux-x64.tar.gz" -C /usr/local --strip-components=1 \
    && rm "node-v$NODE_VERSION-linux-x64.tar.gz" \
    && npm install -g webpack
    
COPY . /app
WORKDIR /app
RUN npm install
WORKDIR /
RUN rm -rf /app
