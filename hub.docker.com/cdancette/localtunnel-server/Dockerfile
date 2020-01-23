FROM mhart/alpine-node:6.3.0

RUN mkdir -p /app
WORKDIR /app

ADD package.json /app/

RUN npm install --production && \
    rm -rf /tmp/* /root/.npm /root/.node-gyp

ADD . /app

ENTRYPOINT ["bin/server"]
