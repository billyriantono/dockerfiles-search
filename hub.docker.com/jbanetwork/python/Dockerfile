FROM alpine:3.9

# if you add shit to this, pay attention to the order.
# we install a full fledged version of python and all the
# tools for pip and then we get rid of them all after we
# install our pip modules and install a minimal python version
# This saves about 200MB of size... we get rid of all the apt files for good measure.
RUN apk add --update --no-cache \
        musl-utils \
        musl-dev \
        musl \
        && \
    apk add --update --no-cache \
        libevent \
        libcouchbase \
        libcouchbase-libevent \
        libcouchbase-dev \
        libcouchbase-bin \
        libressl2.7-libcrypto \
        libressl2.7-libssl \
        python3 \
        build-base \
        python3-dev \
        bash \
        wget \
        ca-certificates \
        && \
    apk add --no-cache --virtual=build-dependencies && \
    wget "https://bootstrap.pypa.io/get-pip.py" -O /dev/stdout | python3 && \
    pip3 install \
        couchbase \
        # docker-py==1.10.6 \ i THINK compose will install this for us
        httplib2 \
        redis===2.10.6 \
        redis-py-cluster \
        pymongo \
        PyMySQL \
        pympler \
        sh \
        kombu==4.1.0 \
    && \
    pip3 install -U "celery[redis]==4.1.0" && \
    apk del build-dependencies build-base python3-dev && \
    rm -r /root/.cache && \
    rm -r /usr/share/terminfo
