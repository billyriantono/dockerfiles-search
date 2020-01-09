FROM node:8

WORKDIR /dashboard

COPY package*.json ./
COPY yarn.lock ./

RUN npm i -g yarn
RUN yarn

COPY . .

CMD [ "yarn", "run", "start" ]