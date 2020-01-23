FROM hackyo/debian
MAINTAINER hackyo <137120918@qq.com>
ENV NODE_HOME /usr/local/nodejs
ENV PATH $NODE_HOME/bin:$NODE_HOME/node-global/bin:$PATH
ADD https://nodejs.org/dist/v10.15.3/node-v10.15.3-linux-x64.tar.xz /nodejs/
RUN apt-get install -y xz-utils && apt-get clean && apt-get autoremove \
    && cd /nodejs \
    && xz -d node-v10.15.3-linux-x64.tar.xz \
    && tar xf node-v10.15.3-linux-x64.tar \
    && mv node-v10.15.3-linux-x64 /usr/local/nodejs \
    && cd / \
    && rm -rf nodejs \
    && mkdir /usr/local/nodejs/node-global \
    && mkdir /usr/local/nodejs/node-cache \
    && npm config set prefix "/usr/local/nodejs/node-global" \
    && npm config set cache "/usr/local/nodejs/node-cache" \
    && npm config set registry "https://registry.npm.taobao.org" \
    && node -v \
    && npm -v
CMD ["bash"]
