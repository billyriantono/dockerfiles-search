FROM node:alpine

# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
COPY package*.json ./

RUN npm install
RUN npm install -g @angular/cli

# Bundle app source
COPY . .

# build prod package
RUN ng build --prod

EXPOSE 8080

CMD ["npm", "start"]
