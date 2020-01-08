FROM node:7.1.0

RUN ["mkdir", "-p", "/usr/src/app"]

WORKDIR /usr/src/app

COPY . /usr/src/app

RUN npm install

RUN npm run build

CMD ["npm", "run", "production"]
