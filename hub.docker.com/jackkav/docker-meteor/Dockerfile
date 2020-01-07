FROM philipgraf/meteor-pdf
MAINTAINER Jack Kavanagh <jack.kavanagh@digitalpublishing.cn>
RUN apt-get update \
        && apt-get install -y --no-install-recommends \
                openjdk-7-jre-headless \
                graphicsmagick \
                libicu48 \
                ttf-arphic-uming \
                ttf-arphic-ukai \
                ttf-wqy-zenhei \
        && rm -rf /var/lib/apt/lists/*
