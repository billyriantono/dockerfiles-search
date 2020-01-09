FROM mhart/alpine-node:latest

RUN mkdir -p /src

WORKDIR /src

COPY package.json .

RUN npm i

COPY . .

EXPOSE 80

CMD ["npm", "start"]
