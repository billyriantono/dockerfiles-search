FROM greyfoxit/alpine-android
WORKDIR /app
ADD . /app
RUN mkdir /usr/lib/gradle

ENV GRADLE_VERSION 2.13
ENV GRADLE_HOME /usr/lib/gradle/gradle-${GRADLE_VERSION}
ENV PATH ${PATH}:${GRADLE_HOME}/bin

WORKDIR /usr/lib/gradle
RUN set -x \
  && apk add --no-cache wget \
  && wget https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip \
  && unzip gradle-${GRADLE_VERSION}-bin.zip \
  && rm gradle-${GRADLE_VERSION}-bin.zip \
  && apk del wget

RUN apk update && apk add bash libstdc++ && rm -rf /var/cache/apk/*

RUN apk --update add wget curl git php7 php7-fpm php7-json php7-phar php7-iconv php7-openssl php7-zlib php7-dom php7-mbstring php7-tokenizer php7-gd php7-fileinfo php7-xml php7-pdo_mysql
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin --filename=composer 
RUN apk --no-cache add bash openssh 
RUN apk --no-cache add nodejs nodejs-npm
RUN apk --no-cache add python python-dev py-pip build-base && pip install virtualenv && rm -rf /var/cache/apk/* 
RUN npm install -g cordova ionic 
RUN npm install -g gulp gulp-cli grunt grunt-cli
