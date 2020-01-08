FROM node:carbon

# Create app directory
WORKDIR /usr/src/app
# Bundle app source
COPY . .
# Install dependencies
RUN yarn install

CMD [ "node", "src/index.js" ]