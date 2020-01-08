FROM node:8
# Create app directory
WORKDIR /src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 8018
CMD [ "npm", "start" ]
