FROM node:latest
ARG TEST=0.12.12

RUN npm install -g git-cache-http-server

ADD init.sh /init.sh
RUN chmod 700 /init.sh

VOLUME [ "/tmp/cache/git" ]

ENTRYPOINT [ "/init.sh" ]
