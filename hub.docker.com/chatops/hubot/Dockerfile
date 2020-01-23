FROM node:4

ENV HUBOT_VERSION 2.18.0

RUN mkdir /bot && \
    useradd -ms /bin/bash node && \
    chown -R node /bot && \
    npm install -g hubot@${HUBOT_VERSION} yo@1.7.0 generator-hubot@0.3.1

USER node
WORKDIR /bot

RUN cd /bot && yo hubot --defaults

CMD ["./bin/hubot"]