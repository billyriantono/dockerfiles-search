FROM google/nodejs
MAINTAINER Marcel Grossmann <whatever4711@gmail.com>
LABEL architecture="amd64"

WORKDIR /app
RUN apt-get update && apt-get install unzip
ADD https://github.com/Dash-Industry-Forum/dash.js/archive/v1.3.0.zip v1.3.0.zip

RUN unzip v1.3.0.zip

WORKDIR /app/dash.js-1.3.0

RUN npm install -g grunt-cli
RUN npm install grunt-template-jasmine-istanbul --save-dev
RUN npm install grunt-contrib-connect grunt-contrib-watch
RUN npm install grunt-contrib-jshint grunt-contrib-uglify
RUN npm install grunt-jsdoc-plugin grunt-jsdoc

#TODO install NPM dependencies
#RUN grunt --config Gruntfile.js --force
