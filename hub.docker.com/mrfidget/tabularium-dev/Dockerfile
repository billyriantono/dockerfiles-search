FROM node:6.14-alpine
WORKDIR /app
COPY package.json /app
RUN npm install
COPY . /app
CMD npm run devstart
EXPOSE 3003