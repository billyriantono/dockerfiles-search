# depends on node latest
FROM node:latest

# author information
MAINTAINER kingslam<linsiyang@touna.cn>

# create workspace
RUN mkdir -pv /data/apps
WORKDIR /data/apps

# install taobao mirror
RUN npm install cnpm -g --registry=https://registry.npm.taobao.org

# install http-server
# install vue pack
# install webpack
# install axios+sass+store
RUN cnpm install -g http-server bower grunt grunt-reload grunt-cli axios vuex vue-cli vue-router vue-lazyload webpack webpack-dev-server webpack-cli node-sass sass-loader jquery

# install productive environment
RUN cnpm install -S better-scroll babel-polyfill jsonp element-ui

# install development environment
RUN cnpm install -D fastclick
