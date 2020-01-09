FROM node:10

# Create app directory
WORKDIR /c/Users/hecto/Documents/Master/DespliegueOperServicios

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm install --only=production

# Bundle app source
COPY . .

#VOLUME /c/Users/hecto/Documents/Master/DespliegueOperServicios/data

VOLUME /c/Users/hecto/Documents/Master/DespliegueOperServicios/logs

EXPOSE 8080
CMD [ "npm", "start" ] 