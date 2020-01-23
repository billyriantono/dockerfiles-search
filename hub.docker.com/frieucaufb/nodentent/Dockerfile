FROM node:10

WORKDIR /usr/src/app

EXPOSE 4002

COPY package.json package-lock.json* ./

RUN npm install
RUN npm cache clean --force

COPY . . 

# ENV json1 test1.json

CMD [ "node", "index.js" ]