FROM donhenton/maven-docker

RUN rm -rf /var/cache/apk/* && \
    rm -rf /tmp/*

RUN apt-get update && \
apt-get install -y ruby python

RUN npm install node-sass
