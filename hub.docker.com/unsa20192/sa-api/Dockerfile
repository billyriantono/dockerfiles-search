FROM node:carbon-slim

# Create app directory
WORKDIR /sa-api

# Install app dependencies
COPY package.json /sa-api/
RUN npm install

# Bundle app source
COPY . /sa-api/
RUN npm run prepublish

ENV PORT=5000
ENV SHOW_URLS=true
ENV AUTH_URL=10.0.2.15
ENV AUTH_PORT=4000
ENV AUTH_USERS_ENTRY=sa-auth-ms/resources/users

EXPOSE 5000

CMD [ "npm", "run", "runServer" ]
