FROM node:9.3.0-slim
RUN wget -c "http://mirrors.163.com/.help/sources.list.wheezy" && cp sources.list.wheezy /etc/apt/sources.list \
    && apt-get update && apt-get install -y python nginx curl \
    && npm config set registry https://registry.npm.taobao.org \
    && npm cache verify \
    && npm install -g @angular/cli --unsafe-perm \
    && ng version 
