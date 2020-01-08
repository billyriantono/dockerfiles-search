FROM bconnect/gitlab-base

ENV CHROMEDRIVER_VERSION 2.46
RUN apk add --update php7-pdo
RUN apk add --update php7-pdo_mysql
RUN apk add --update php7-tokenizer
RUN apk add --update php7-session
RUN apk add --update php7-xml
RUN apk add --update php7-xmlwriter
RUN apk add --update php7-gd
RUN apk add --update mysql mysql-client
RUN apk add libexif udev chromium chromium-chromedriver xvfb openjdk8-jre mysql
RUN npm config set user 0
RUN npm config set unsafe-perm true
RUN npm install -g selenium-side-runner
RUN wget https://selenium-release.storage.googleapis.com/3.141/selenium-server-standalone-3.141.59.jar
RUN mv selenium-server-standalone-3.141.59.jar /selenium.jar
