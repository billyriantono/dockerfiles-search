FROM node:10

# Create app directory
WORKDIR /usr/src/app

#RUN npm install
RUN npm install --save express ejs

# Bundle app source
COPY . .

EXPOSE 8000
CMD node bestbuy.ca.js
