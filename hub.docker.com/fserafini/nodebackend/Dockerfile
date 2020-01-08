FROM node:alpine
MAINTAINER FS. <fsm.systems>

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
#COPY package*.json ./

#RUN npm install
# If you are building your code for production
# RUN npm install --only=production

# Bundle app source
#COPY . .

RUN apk update && apk upgrade && \
    apk add --no-cache bash git openssh
    
ENV TERM="xterm" \
    DB_HOST="mongo" \
    DB_NAME="" \
    DB_USER=""

EXPOSE 9091
CMD [ "npm", "start" ]                        
