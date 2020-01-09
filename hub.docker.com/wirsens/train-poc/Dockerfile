# FROM node:argon

# # Create app directory
# RUN mkdir -p /usr/src/app
# WORKDIR /usr/src/app

# # Install app dependencies
# COPY package.json /usr/src/app/
# RUN npm install
# RUN npm install bower
# RUN bower install

# # Bundle app source
# COPY . /usr/src/app

# EXPOSE 80
# CMD [ "npm", "start" ]
FROM nginx
COPY build/default /usr/share/nginx/html
EXPOSE 80
