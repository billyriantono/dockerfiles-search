FROM node:10

#App directory
WORKDIR /usr/src/app

#Install dependencies
COPY package*.json ./

RUN npm install
# RUN npm ci -- production builds

#Bundle source
COPY . .

#Expose ports
EXPOSE 8080

#Start application
CMD ["npm", "run", "start"]
