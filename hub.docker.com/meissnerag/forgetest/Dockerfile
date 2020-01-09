FROM node:latest

# Create app directory
RUN mkdir /forgetest
WORKDIR /forgetest

# Add a /app volume
#VOLUME ["/pia"]

# Define working directory
#WORKDIR /pia

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

#RUN npm install -g npm
RUN npm install
# If you are building your code for production
# RUN npm install --only=production

# Bundle app source
COPY . .

#NPM Update
RUN npm i -g npm

EXPOSE 8080
CMD [ "npm", "start" ]
