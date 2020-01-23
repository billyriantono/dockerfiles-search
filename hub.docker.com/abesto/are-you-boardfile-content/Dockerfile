FROM node:11.10.0
# Create app directory
WORKDIR /usr/src/app
# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./
RUN yarn install
# Bundle app source
COPY . .
EXPOSE 49151
CMD [ "yarn", "start" ]