FROM node:latest

# Create App Directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Install App Dependencies
COPY package.json /usr/src/app/
RUN npm install

# Add App Source
COPY . /usr/src/app

# Build APp
RUN npm run build

EXPOSE 8080
CMD npm start -- --config /usr/src/app/configs/config.json
