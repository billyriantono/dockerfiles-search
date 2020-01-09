FROM node:latest
MAINTAINER Jan Philip Schellenberg <jps@Lumi.education>

# Adding source files into container
ADD . /srv

# Define working directory
WORKDIR /srv

# Install app dependencies & build
RUN npm install
RUN npm run build

# Open Port 3000
EXPOSE 80

# Run Node.js
CMD ["node", "build/index.js"]
