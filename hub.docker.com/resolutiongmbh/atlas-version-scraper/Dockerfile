FROM node:10

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./

# Install prod dependencies
RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 8000
ENTRYPOINT [ "npm", "run" ]
CMD [ "server" ]
