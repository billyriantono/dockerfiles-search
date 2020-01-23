FROM node:7.7.3

RUN npm install create-elm-app -g

COPY package.json /usr/src/app/
RUN npm install

COPY . /usr/src/app
WORKDIR /usr/src/app
RUN npm run build

EXPOSE 3000

CMD ["npm", "start"]

