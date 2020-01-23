FROM node:7.0.0-onbuild

ENV term=xterm

RUN npm install && \
    npm install chalk && \
    npm link

ENTRYPOINT [  "example-cli" ]
