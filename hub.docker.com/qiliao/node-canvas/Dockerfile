FROM registry.cn-hangzhou.aliyuncs.com/aliyun-node/alinode:3.11.0

WORKDIR /app
RUN yarn add canvas@next canvas-prebuilt@next
RUN rm yarn.lock \
    && cp /app/node_modules/canvas/build/Release/canvas.node /app/node_modules/canvas/build/Release/canvas-prebuilt.node \
    && cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
RUN yarn config set registry https://registry.npm.taobao.org
