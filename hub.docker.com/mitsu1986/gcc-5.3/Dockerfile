FROM gliderlabs/alpine:latest

RUN apk --no-cache add cmake build-base git bash \
        && mkdir -p /tmp/src \
        && cd /tmp/src \
        && git clone git://github.com/cpputest/cpputest.git \
        && cd cpputest \
        && cmake -DMAP_FILE=ON -DCOVERAGE=ON -DC++11=ON \
        && make \
        && make install \
        && cd \
        && rm -rf /tmp/src \
        && apk del --purge git

ENTRYPOINT ["/bin/bash", "-c"]



