FROM node:carbon

WORKDIR /app

COPY package.json .
COPY yarn.lock .

RUN yarn 

COPY index.js /app

CMD [ "node", "index.js" ]
