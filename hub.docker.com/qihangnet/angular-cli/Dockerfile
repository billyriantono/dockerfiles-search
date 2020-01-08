FROM node:alpine
RUN npm config set registry https://registry.npm.taobao.org \
    && npm install -g @angular/cli@6.2.4 \
    && apk add --no-cache python
RUN npm install --unsafe-perm=true -g node-sass