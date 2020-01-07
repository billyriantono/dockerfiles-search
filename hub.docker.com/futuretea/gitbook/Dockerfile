FROM node:6-slim
RUN npm config set registry https://registry.npm.taobao.org \
    && npm install -g gitbook-cli \
    && gitbook fetch 2.6.7
