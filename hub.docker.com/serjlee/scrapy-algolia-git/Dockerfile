FROM alpine:3.6

ENV CFLAGS="-O0" 
ENV LIBRARY_PATH=/lib:/usr/lib
ENV RUNTIME_PACKAGES python py-pip libxslt libxml2 zlib git curl openssl
ENV BUILD_PACKAGES   build-base libxslt-dev libxml2-dev libffi-dev \
                     zlib-dev python-dev openssl-dev
ENV PYTHON_PACKAGES  git+https://github.com/scrapy/scrapy.git \
                     pyopenssl \
                     python-slugify \
                     algoliasearch \
                     dateparser
RUN \
  apk add --no-cache ${RUNTIME_PACKAGES} ${BUILD_PACKAGES} && \
  pip install -U pip && \
  pip install ${PYTHON_PACKAGES} && \
  apk del ${BUILD_PACKAGES} && \
  rm -rf /root/.cache
