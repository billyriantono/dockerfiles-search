FROM node:8
WORKDIR /usr/src/app
RUN apt-get update && \
    apt-get install curl -y && \
    curl -fsSL get.docker.com -o get-docker.sh && \
    sh get-docker.sh
COPY package.json .
RUN npm install
COPY index.js .
COPY config.json .
COPY npm-shrinkwrap.json .
EXPOSE 80
CMD [ "npm", "start" ]