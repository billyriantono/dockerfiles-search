FROM node:10-alpine

WORKDIR /app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./
COPY . .


RUN npm run package
# If you are building your code for production
# RUN npm ci --only=production

USER node
# Bundle app source

# EXPOSE 4000

CMD [ "npm", "start" ]