FROM alpine:latest

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" > /etc/apk/repositories \
&& echo "http://dl-cdn.alpinelinux.org/alpine/edge/community" >> /etc/apk/repositories \
&& echo "http://dl-cdn.alpinelinux.org/alpine/edge/main" >> /etc/apk/repositories \
&& apk add --update --no-cache nodejs-npm python3 zip \
&& npm install -g yarn \
&& if [[ ! -e /usr/bin/python ]]; then ln -sf /usr/bin/python3 /usr/bin/python; fi \
&& if [[ ! -e /usr/bin/pydoc ]]; then ln -sf /usr/bin/pydoc3 /usr/bin/pydoc; fi \
&& if [[ ! -e /usr/bin/easy_install ]]; then ln -sf /usr/bin/easy_install-* /usr/bin/easy_install; fi \
&& easy_install pip \
&& if [[ ! -e /usr/bin/pip ]]; then ln -sf /usr/bin/pip3 /usr/bin/pip; fi \
&& pip install --upgrade pip \
&& pip install boto3==1.3.0 \
&& apk del curl make gcc g++ linux-headers binutils-gold gnupg \
&& rm -rf /usr/include /usr/share/man /tmp/* /var/cache/apk/* /root/.npm /root/.node-gyp /root/.gnupg /usr/lib/node_modules/npm/man /usr/lib/node_modules/npm/doc /usr/lib/node_modules/npm/html /usr/lib/node_modules/npm/scripts