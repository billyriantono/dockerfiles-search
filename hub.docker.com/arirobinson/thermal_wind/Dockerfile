FROM node:10

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

ENV DARKSKY_KEY=123 \
    MONGO_URL=mongodb://0.0.0.0:27017/ \
    UPDATE_DELAY=10 \
    TZ=America/Vancouver

EXPOSE 8080
CMD [ "node", "server.js" ]