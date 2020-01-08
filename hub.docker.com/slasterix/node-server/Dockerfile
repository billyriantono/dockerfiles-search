FROM node:latest

# Create app directory
RUN mkdir -p /my_app
WORKDIR /my_app
COPY package.json /my_app
COPY package*.json /my_app

RUN cd /my_app
RUN npm install
#RUN npm install -g express --save \
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . /my_app

EXPOSE 6001
#CMD [ "node", "server.js" ]
#CMD ["npm", "start"]
