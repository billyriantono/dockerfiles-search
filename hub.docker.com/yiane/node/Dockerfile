ARG NODE_VERSION=12
FROM node:${NODE_VERSION}
MAINTAINER <yiane@qq.com>

RUN mkdir -p /var/www/html && \
    mkdir -p /opt/node/node_global && \
    mkdir -p /opt/node/node_cache && \
    chown -R node.node /opt/node && \
    npm config set registry https://registry.npm.taobao.org --global && \
    npm config set disturl https://npm.taobao.org/dist --global && \
    npm config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/ --global && \
    npm config set phantomjs_cdnurl http://npm.taobao.org/mirrors/phantomjs --global && \
    npm config set ELECTRON_MIRROR http://npm.taobao.org/mirrors/electron/ --global && \
    npm config set prefix "/opt/node/node_global" --global && \
    npm config set cache "/opt/node/node_cache" --global && \
#    npm install -g react-native-cli node-sass && \
    yarn config set registry https://registry.npm.taobao.org --global && \
    yarn config set disturl https://npm.taobao.org/dist --global && \
    yarn config set sass_binary_site https://npm.taobao.org/mirrors/node-sass/ --global && \
    yarn config set phantomjs_cdnurl http://npm.taobao.org/mirrors/phantomjs --global && \
    yarn config set ELECTRON_MIRROR http://npm.taobao.org/mirrors/electron/ --global && \
    yarn config set prefix "/opt/node/yarn_global" --global && \
    yarn config set cache "/opt/node/yarn_cache" --global

#    npm config ls -l&& \
#    yarn config list && \
USER node
# 创建镜像的时候并不会挂载目录。所以全局安装无效，只能在初始化脚本里进行安装
# 或者，不挂载global目录到属主机（生产环境推荐不挂载）
# RUN npm install -g react-native-cli node-sass && yarn global add react-native-cli node-sass
RUN yarn config set prefix "/opt/node/yarn_global" && \
    yarn config set cache "/opt/node/yarn_cache"

WORKDIR /var/www/html

VOLUME ["/var/www/html", "/opt/node"]

CMD ["node"]
