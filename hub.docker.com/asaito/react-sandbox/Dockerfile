FROM node:latest

WORKDIR /srv/package

COPY public ./public
COPY src ./src
COPY package.json README.md ./

RUN npm i --verbose --no-package-lock --build-from-source
EXPOSE 3000

CMD npm run start
