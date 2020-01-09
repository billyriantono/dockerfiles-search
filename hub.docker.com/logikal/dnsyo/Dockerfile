FROM gliderlabs/alpine

RUN apk-install \
        python \
        python-dev \
        py-pip \
        build-base \
      && pip install dnsyo

CMD ["dnsyo", "--help"]

