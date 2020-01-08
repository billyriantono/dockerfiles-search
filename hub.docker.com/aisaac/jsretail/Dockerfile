FROM mhart/alpine-node:8

WORKDIR /app

# Install packages
COPY package*.json ./

RUN npm install --production

# copy app files
COPY . .

EXPOSE 8080
CMD [ "node", "server.js" ]