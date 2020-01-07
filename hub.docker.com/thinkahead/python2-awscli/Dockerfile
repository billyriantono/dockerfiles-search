FROM alpine:3.7
MAINTAINER Ahead Labs

RUN echo "===> Installing packages"  && \
    apk --update --no-cache add \
    python \
    python-dev \
    build-base \
    py-pip \
    jq \
    bash \
    git \
    groff \
    less \
    mailcap \
    bash \
    g++ \
    gcc \
    libxslt-dev


RUN echo "===> Adding python modules and tidying up..."  && \
    rm -r /usr/lib/python*/ensurepip \
    && pip install --upgrade pip setuptools beautifulsoup4\
    && pip install --no-cache-dir awscli \
    && rm -rf /var/cache/apk/* /root/.cache/pip/*

# ONBUILD RUN /env/bin/pip install -r requirements.txt


# change default shell from ash to bash
RUN echo "===> Changing default shell to bash"  && \
    sed -i -e "s/bin\/ash/bin\/bash/" /etc/passwd

WORKDIR /root
VOLUME /root/.aws

ENTRYPOINT [ "aws" ]
CMD ["--version"]
