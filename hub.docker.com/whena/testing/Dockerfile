FROM node:8

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm install --only=production

#daemon for cron jobs
RUN echo 'echo will install crond...' >> /usr/src/start.sh -C
RUN echo 'crond' >> /usr/src/start.sh -C

# Bundle app source
COPY . .

EXPOSE 8080
CMD [ "npm", "start" ]
