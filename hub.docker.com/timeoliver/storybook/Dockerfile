FROM node:10-alpine

MAINTAINER toliu<1928385951@qq.com>

COPY . /storybook

WORKDIR /storybook

VOLUME ["/storybook/src"]

EXPOSE 8080

RUN yarn --registry https://registry.npm.taobao.org install && \
    chmod +x /storybook/tool/start.sh

CMD /storybook/tool/start.sh