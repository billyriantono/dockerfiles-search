FROM node:10

# App directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package.json ./

ARG TOKEN
ENV TOKEN=$TOKEN

RUN npm install

COPY . .

CMD [ "node", "index.js" ]