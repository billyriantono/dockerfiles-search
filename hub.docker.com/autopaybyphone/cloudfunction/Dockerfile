FROM openwhisk/dockerskeleton

WORKDIR /action/

RUN curl -Lo phantom.tgz https://github.com/DarthHater/docker-phantomjs2/releases/download/2.1.1/dockerized-phantomjs.tar.gz && \
tar xzf phantom.tgz -C / && \
rm phantom.tgz && \
curl -Ls "https://github.com/dustinblackman/phantomized/releases/download/2.1.1/dockerized-phantomjs.tar.gz" | tar xz -C / && \
ln -s $(which phantomjs) "/action/phantomjs" && \
curl -Ls "https://github.com/casperjs/casperjs/tarball/1.1.0" | tar xz && \
mv casperjs-casperjs-b5c59e1 casperjs

WORKDIR /

