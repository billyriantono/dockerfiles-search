FROM node:9

MAINTAINER X3Y <changhongbo0812@gmail.com>

# use cnpm
RUN npm install -g cnpm \
	--registry=https://registry.npm.taobao.org \
	&& cnpm install --quiet vue \
	&& cnpm install --quiet --global vue-cli \
	&& cnpm install --quiet --global @vue/cli-service \
	&& ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

