

# specify the node base image with your desired version node:<version>
FROM node:8.9.1
WORKDIR /
COPY package.json /
RUN npm install
COPY . /
CMD [ "npm", "start" ]
# replace this with your application's default port
EXPOSE 3004
