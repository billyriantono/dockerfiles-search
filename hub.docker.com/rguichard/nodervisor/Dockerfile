FROM alpine:3.1

MAINTAINER Romain Guichard <rguichard@vsense.fr>

RUN apk --update add \
    git \
    supervisor \
    nodejs

RUN git clone https://github.com/TAKEALOT/nodervisor /nodervisor

WORKDIR /nodervisor

RUN apk --update add --virtual deps \
    coreutils \
    build-base \
    gcc \
    make && \
    npm install express --global && \
    npm install && \
    apk del deps

COPY supervisord.conf /etc/supervisord.conf
COPY supervisord-nodervisor.ini /etc/supervisor.d/supervisord-nodervisor.ini

EXPOSE 3000

CMD ["supervisord", "-c", "/etc/supervisord.conf", "-n"]
