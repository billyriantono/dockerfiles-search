FROM alpine:3.8
MAINTAINER FAN VINGA<fanalcest@gmail.com>

ENV ADMIN_NAME=admin         \
    ADMIN_PASSWORD=password  \
    PASSWORD_SALT=salt 	     \
    PROTOCOL=wss

RUN apk --no-cache add git nodejs nodejs-npm       && \
    git clone https://github.com/hack-chat/main --depth 1 && \
    cd main/server && npm install && cd /main             && \
    ln -s /main/client /app                               && \
    rm -rf .git clientSource documentation

ADD config.json /main/server/config/config.json
ADD nginx.conf  /etc/nginx/nginx.conf

RUN mkdir /main/origconf && \
    mv /main/client/client.js /main/origconf && \
    mv /main/server/config/config.json /main/origconf &&\
    ln -s /tmp/client.js /main/client/client.js && \
    ln -s /tmp/config.json /main/server/config/config.json

WORKDIR /main/server
EXPOSE 6060

USER chat
ENV USER=chat

CMD cp /main/origconf/* /tmp && \
    #mkdir /var/tmp/nginx && \
    #mkdir /var/lib/nginx/proxy && \
    sed -i "s|ws://|${PROTOCOL}://|g"             /tmp/client.js   && \
    sed -i "s/ADMIN_NAME/${ADMIN_NAME}/g"         /tmp/config.json && \
    sed -i "s/ADMIN_PASSWORD/${ADMIN_PASSWORD}/g" /tmp/config.json && \
    sed -i "s/PASSWORD_SALT/${PASSWORD_SALT}/g"   /tmp/config.json && \
    node main.js
