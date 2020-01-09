FROM node

WORKDIR /usr/build
COPY package.json .
RUN npm i
COPY . .
RUN npm run build

WORKDIR /usr/wutucall
RUN mv /usr/build/dist .
RUN mv /usr/build/node_modules .
RUN rm -rf ./usr/build
COPY package.json .
COPY server.js .

ENV PORT=80
EXPOSE 80
CMD [ "npm", "run", "serve" ]
