FROM alpine:3.8

RUN echo http://mirrors.aliyun.com/alpine/v3.8/main > /etc/apk/repositories && \
    echo http://mirrors.aliyun.com/alpine/v3.8/community >> /etc/apk/repositories

RUN apk update && \
    apk add --no-cache python python-dev py-pip git nodejs npm gcc make bash && \
    pip install --upgrade pip && \
    pip install pymongo && \
    mkdir /yapi && cd /yapi && \
    git clone https://github.com/YMFE/yapi.git vendors && \
    cd vendors && \
    npm install --production --registry https://registry.npm.taobao.org

WORKDIR /yapi/vendors

COPY files/config.json /yapi/
COPY files/entrypoint.sh /
COPY files/check-mongo-init.py /
COPY files/init-mongo.py /

RUN chmod +x /entrypoint.sh && \
    chmod +x /check-mongo-init.py && \
    chmod +x /init-mongo.py

EXPOSE 3000

ENTRYPOINT ["/entrypoint.sh"]
