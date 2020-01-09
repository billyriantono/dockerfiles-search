FROM node:10

# Create app directory
RUN mkdir -p /usr/src/app
RUN wget https://github.com/n-agency/status-worker/archive/1.1.zip
RUN unzip 1.1.zip -d /usr/src/
WORKDIR /usr/src/status-worker-1.1

# Install app dependenciesnpm
RUN npm install

CMD [ "npm", "run", "dev" ]
