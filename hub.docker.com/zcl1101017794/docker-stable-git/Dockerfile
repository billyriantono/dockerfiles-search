FROM docker:19.03.1-dind
ADD mime.types /etc/mime.types
ADD mime.types ~/mime.types
RUN echo "ipv6" >> /etc/modules
RUN echo "http://dl-1.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories;
RUN echo "http://dl-2.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories;
RUN echo "http://dl-3.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories;
RUN echo "http://dl-4.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories;
RUN echo "http://dl-5.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories;
RUN apk add --update alpine-sdk
RUN apk add --update bash autoconf automake lcms2-dev libpng-dev
RUN apk add --update py-pip
RUN apk add --update nodejs
RUN apk add --update npm
RUN npm install yarn -g
RUN wget -P /usr/bin/ http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/50452/cn_zh/1524643963683/ossutil64
RUN chmod 755 /usr/bin/ossutil64
RUN ls /usr/bin/ossutil64
RUN mkdir /lib64 && ln -s /lib/libc.musl-x86_64.so.1 /lib64/ld-linux-x86-64.so.2
RUN apk add python
RUN wget  https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip install s3cmd
RUN pip install awscli
RUN pip install requests
RUN apk add jq
