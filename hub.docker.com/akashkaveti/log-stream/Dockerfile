FROM node:8
USER root
# Create app directory
WORKDIR /usr/src/app
ENV FILE_LOCATION=${FILE_LOCATION}
# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
# COPY package*.json ./

# RUN npm install
# If you are building your code for production
# RUN npm ci --only=production

# Bundle app source
COPY . .

EXPOSE 3000
CMD [ "sh", "-c", "node server.js ${FILE_LOCATION}" ]