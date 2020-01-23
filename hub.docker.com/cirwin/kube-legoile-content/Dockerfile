FROM node
MAINTAINER cinos81@gmail.com
ENV REFRESHED_AT 2017-03-18

RUN mkdir /app
COPY ./package.json /app
COPY ./index.js /app
COPY ./wait-for-it.sh /app
WORKDIR /app
RUN npm install
CMD node index.js