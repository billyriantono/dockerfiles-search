FROM node:argon

# Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app

# Bundle app source
COPY . /usr/src/app

# Set environment
ENV NODE_ENV production

# Install dependencies
RUN npm install

EXPOSE 80
CMD [ "npm", "start" ]