# Adapted from https://nodejs.org/en/docs/guides/nodejs-docker-webapp/
FROM node:10.1.0

# Create frontend directory
WORKDIR /usr/seed-web/frontend

# Install app dependencies
COPY ./app/package*.json ./
RUN npm install

# Bundle app source
COPY ./app/public ./public
COPY ./app/src ./src

# Specify PORT default value
ENV PORT=8000
EXPOSE ${PORT}
CMD [ "npm", "run", "start" ]
