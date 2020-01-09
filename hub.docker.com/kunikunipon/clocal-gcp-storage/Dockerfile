FROM node:8

# Create app directory
WORKDIR /usr/src/app

COPY src/services/cloud-storage/package.json ./
COPY src/services/cloud-storage/yarn.lock ./
COPY src/services/cloud-storage/scripts scripts/
COPY src/services/cloud-storage/*.js ./

RUN yarn

EXPOSE 8080

CMD [ "npm", "start" ]