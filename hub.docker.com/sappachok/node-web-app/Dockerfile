FROM node:8

# Create app directory
WORKDIR /nodeapp

# Install app dependencies
# A wildcard is used to ensure both package.json AND package-lock.json are copied
# where available (npm@5+)
COPY app /nodeapp

RUN npm install
# If you are building your code for production
# RUN npm install --only=production

RUN npm install --unsafe-perm -g localtunnel

EXPOSE 3000
CMD [ "npm", "start" ]