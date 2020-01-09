FROM node:8
MAINTAINER Liviu Dobrea <liviu.dobrea@wekode.tech>

# Install dependencies and cache the package.json and package-lock.json
ADD package*.json /tmp/
CMD ["npm", "install", "yarn"]
RUN cd /tmp && yarn install
RUN mkdir -p /usr/src/app && cp -a /tmp/node_modules /usr/src/app/

# Switch to default workspace and add the rest of project there
WORKDIR /usr/src/app
ADD . /usr/src/app
RUN npm run build

# Expose app on :8080 and run it
EXPOSE 8080
CMD ["npm", "start"]