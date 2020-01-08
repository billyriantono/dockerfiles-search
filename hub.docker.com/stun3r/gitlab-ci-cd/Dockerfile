FROM node:10.16.0-alpine

RUN apk --no-cache -q add --virtual native-deps \
  g++ gcc libgcc libstdc++ linux-headers autoconf automake make nasm python build-base binutils libtool zlib-dev openssh && \
  npm install --unsafe-perm --quiet node-gyp -g

RUN npm install --unsafe-perm -g node-sass
RUN npm install --unsafe-perm -g yarn

CMD ["/bin/bash"]
