FROM balenalib/raspberry-pi2-alpine-node:10

RUN [ "cross-build-start" ]
WORKDIR /usr/src/app

RUN apk add --update python3
RUN pip3 install pyserial

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# Bundle app source
COPY . .

RUN npm run flow:build

EXPOSE 8080

CMD [ "node", "build/index.js" ]
RUN [ "cross-build-end" ]