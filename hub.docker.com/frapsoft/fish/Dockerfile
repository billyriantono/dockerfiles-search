FROM node:lts
MAINTAINER frankqcc

ENV LANG C.UTF-8

RUN sed -i s@deb.debian.org@mirrors.aliyun.com@g /etc/apt/sources.list \
        && sed -i s@security.debian.org@mirrors.aliyun.com@g /etc/apt/sources.list \
        && sed -i s@httpredir.debian.org@mirrors.aliyun.com@g /etc/apt/sources.list \
        && sed -i s@cdn-fastly.deb.debian.org@mirrors.aliyun.com@g /etc/apt/sources.list \
        && echo "deb http://mirrors.ustc.edu.cn/debian/ stretch main" >> /etc/apt/sources.list \
        && echo "deb http://mirrors.ustc.edu.cn/debian/ stretch-updates main" >> /etc/apt/sources.list \
        && npm config set registry http://registry.npm.taobao.org/ \
        && mkdir /api \
        && cd /api \
        && git clone -b fine --depth=1 https://github.com/congqiu/yapi.git vendors \
        && cp /api/vendors/config_example.json /api/config.json \
        && cd /api/vendors \
        && npm install --production --registry \
        && npm i -g yapi-cli ykit
        
ENV TZ="Asia/Shanghai" HOME="/api/vendors"
WORKDIR ${HOME}
EXPOSE 3000
ENTRYPOINT ["node"]
