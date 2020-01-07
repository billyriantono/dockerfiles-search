FROM node:8

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY app ./app
COPY environment ./environment
COPY .babelrc .babelrc

RUN npm run build

EXPOSE 9000
CMD ["node", "app/index.js"]
