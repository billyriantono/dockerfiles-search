FROM node:latest
LABEL maintainer="julien.senon@gmail.com"
LABEL version="0.2"
LABEL description="Revealjs Docker"


RUN apt-get update \
    && apt-get install git

RUN git clone https://github.com/hakimel/reveal.js.git

WORKDIR reveal.js

RUN npm install

EXPOSE 8000

CMD  npm start -- --port=8000
