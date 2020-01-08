FROM node:11
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
RUN npm i express pg
COPY index.js /usr/src/app
EXPOSE 8080
CMD [ "node", "/usr/src/app/index" ]