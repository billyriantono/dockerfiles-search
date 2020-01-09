FROM node:9.11-alpine
ENV NODE_ENV production
WORKDIR /usr/src/app
COPY ["package.json", "package-lock.json*", "npm-shrinkwrap.json*", "./"]
RUN npm install --global typescript prettier ts-node tslint
RUN npm install --production --silent && mv node_modules ../
COPY . .
EXPOSE 3000
CMD npm run full:prod