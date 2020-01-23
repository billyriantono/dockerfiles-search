# Instructions copied from - https://hub.docker.com/_/python/
FROM node:4.5

# Create app directory
RUN mkdir -p /var/www/html/XianLiaoM/
WORKDIR /var/www/html/XianLiaoM/chat_nodejs

# Install app dependencies
# COPY package.json /var/www/html/XianLiaoM/chat_nodejs
# RUN npm install

# Bundle app source
COPY . /var/www/html/XianLiaoM/chat_nodejs

# tell the port number the container should expose
EXPOSE 3000

# run the command
CMD [ "npm", "start" ]
