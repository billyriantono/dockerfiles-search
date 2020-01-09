FROM alpine:3.2

MAINTAINER Pan Jiabang <panjiabang@gmail.com> 

# Install Nginx and Node.js env
RUN apk update
RUN apk add nginx bash
RUN apk add nodejs python make g++ && rm -rf /var/cache/apk/*
RUN npm install hexo -g

COPY bin/* /usr/local/bin/
ADD https://raw.githubusercontent.com/JamesPan/blog-src/master/package.json /tmp/

WORKDIR /tmp/

# Install hexo and dependences
RUN npm install && npm cache clean

CMD ["sh"]
