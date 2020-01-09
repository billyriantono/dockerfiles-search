FROM mhart/alpine-node:latest

WORKDIR /
COPY package.json /package.json
RUN npm i --registry=https://registry.npm.taobao.org

COPY build /build
COPY config /config
COPY src /src
COPY static /static
COPY index.html /index.html

COPY .babelrc /.babelrc
COPY .editorconfig /.editorconfig
COPY .gitattributes /.gitattributes
COPY .postcssrc.js /.postcssrc.js

# config-dev
ENV CONFIG_DEV_API setYourValue
ENV CONFIG_DEV_TOKEN_SOURCE setYourValue
ENV CONFIG_DEV_TOKEN_VERSION setYourValue
ENV CONFIG_DEV_UPLOAD setYourValue
# config-pro
ENV CONFIG_PRO_API setYourValue
ENV CONFIG_PRO_TOKEN_SOURCE setYourValue
ENV CONFIG_PRO_TOKEN_VERSION setYourValue
ENV CONFIG_PRO_UPLOAD setYourValue
# baiduMap
ENV BAIDU_MAP_AK setYourValue

ENV DOCKER=true
EXPOSE 17000
