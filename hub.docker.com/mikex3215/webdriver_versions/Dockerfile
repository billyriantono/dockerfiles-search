FROM node:6.2.2

RUN apt-get update && apt-get install awscli -y && apt-get install nginx -y && apt-get install curl -y

COPY webdriver-versions.js ./
RUN npm install -g protractor@4.0.14
RUN npm install minimist@1.2.0 
RUN node ./webdriver-versions.js --chromedriver 2.31 && \
    webdriver-manager update