FROM node:boron
#Create app directory
RUN mkdir -p /usr/src/app
WORKDIR /usr/src/app
#install app dependencies
COPY package.json /usr/src/app/
RUN npm install
#Bundle Source 
COPY . /usr/src/app

EXPOSE 8080

CMD ["npm","start"]