FROM node:lts-alpine
RUN mkdir -p /usr/src/app/
#RUN mkdir -p /usr/src/app/node_modules && chown -R node:node /usr/src/app
WORKDIR /usr/src/app
COPY package*.json ./
#USER node
RUN npm install
COPY . .
#COPY --chown=node:node . .
EXPOSE 3000
CMD [ "npm", "start" ]