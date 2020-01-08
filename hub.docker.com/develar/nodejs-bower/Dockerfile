FROM develar/nodejs
MAINTAINER Vladimir Krivosheev <develar@gmail.com>

# bower requires git
RUN apk-install git && npm install -g bower
WORKDIR /data

ENTRYPOINT ["bower", "--allow-root", "install"]