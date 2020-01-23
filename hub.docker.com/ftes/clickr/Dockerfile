FROM node:latest

# Create app directory
WORKDIR /usr/src/app

RUN npm install lerna@3 --global --loglevel notice

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./
COPY lerna.json ./
COPY packages/server/package*.json ./packages/server/
COPY packages/client/package*.json ./packages/client/

RUN npm install --only=production --unsafe-perm --loglevel notice
RUN lerna bootstrap

# Bundle app source
COPY packages/server ./packages/server
COPY packages/client ./packages/client

# Build
RUN npm run build

EXPOSE 3000
CMD [ "npm", "run", "production" ]