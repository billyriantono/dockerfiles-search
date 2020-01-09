# build and deploy wallpaper site
FROM node:10

# Create app directory
WORKDIR /usr/src

# create dependences cache layer
COPY package*.json ./

# install local dependences
RUN npm ci

# copy program code resource
COPY . ./

# expose port
EXPOSE 80

CMD export port=80 && npm run deploy:docker
