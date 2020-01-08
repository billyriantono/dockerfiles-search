FROM node:boron

ENV environment dev
ENV dbhost localhost
# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package.json .
RUN npm install

# Bundle app source
COPY . .

EXPOSE 10010

CMD [ "npm", "start" ]
#CMD [ "sh", "-c", "ENVIRONMENT=$environment DBHOST=$dbhost swagger project start" ]