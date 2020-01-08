FROM node

MAINTAINER Bryce Fisher-Fleig

RUN useradd -m -U -s /bin/sh unpriv
RUN mkdir -p /home/unpriv/fakehome && \
    chmod 077 /home/unpriv/fakehome && \
    chown unpriv:unpriv /home/unpriv/fakehome

RUN mkdir -p /home/unpriv/app && \
    chown unpriv:unpriv /home/unpriv/app

WORKDIR /home/unpriv

USER unpriv
ADD app /home/unpriv/app
RUN cd /home/unpriv/app && \
    npm install
