FROM node:8.2.0

WORKDIR /code

ADD package.json /code/package.json

RUN yarn install

COPY . .

EXPOSE 3000

CMD [ "yarn", "start" ]
