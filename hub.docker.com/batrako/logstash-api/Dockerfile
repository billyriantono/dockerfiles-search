FROM node


# Create app directory
WORKDIR /usr/src/app

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY package*.json ./

RUN npm install
# If you are building your code for production
# RUN npm install --only=production

# Bundle app source

COPY . .
RUN chown -R 1000.1000 /usr/src/app
ENV ELASTIC_USERNAME "elastic"
ENV ELASTIC_PASSWORD "changeme"

USER 1000
EXPOSE 8080
CMD [ "npm", "run", "start" ]
