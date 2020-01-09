FROM python:2.7

MAINTAINER Paul Liljenberg "lilenberg.paul@gmail.com"


RUN git clone --depth=1 https://github.com/RuudBurger/CouchPotatoServer.git

EXPOSE 5050

ENTRYPOINT python CouchPotatoServer/CouchPotato.py
