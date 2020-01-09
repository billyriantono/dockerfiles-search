FROM mhart/alpine-node:13.5

WORKDIR /app

COPY package.json /app
COPY yarn.lock /app

RUN yarn install

COPY . /app

RUN yarn build

EXPOSE 3030

ENTRYPOINT ["yarn", "prod"]
