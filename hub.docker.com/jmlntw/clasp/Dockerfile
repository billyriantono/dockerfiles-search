FROM node:alpine

RUN npm install -g @google/clasp

RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
VOLUME /usr/src/app

ENTRYPOINT ["clasp"]
CMD ["--help"]
