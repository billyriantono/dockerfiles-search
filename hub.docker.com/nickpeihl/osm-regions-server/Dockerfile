FROM node:carbon-alpine
LABEL maintainer='Nick Peihl <nick.peihl@elastic.co>'

ENV POSTGRES_DB=gis
ENV POSTGRES_USER=sophox
ENV POSTGRES_PASSWORD=shhh
ENV POSTGRES_HOST=postgres 
ENV POSTGRES_PORT=5432
ENV RDF_HOST=sophox.org 
ENV RDF_PORT=80
ENV OSMREGIONS_PORT=9978
ENV NODE_ENV=production

WORKDIR /usr/src/app

COPY package*.json ./

RUN apk add --no-cache git \ 
    && npm install 

COPY . .

EXPOSE 9978
CMD [ "npm", "start" ]