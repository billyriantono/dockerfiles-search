# https://nodejs.org/de/docs/guides/nodejs-docker-webapp/
FROM node:12.13
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

# Install all packages, including devDependencies
RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
# Copy full src dir to WORKDIR
COPY . .

EXPOSE 8080

# Run directly via node
CMD [ "node", "server.js" ]

# Run via npm
# CMD [ "npm", "run", "dev" ]