FROM ubuntu:xenial

RUN apt-get update -yqq && \
    apt-get install -yqq pdf2htmlex && \
    rm -rf /var/lib/apt/lists/*

COPY ./manifest /usr/share/pdf2htmlEX/

VOLUME /pdf
WORKDIR /pdf

CMD ["pdf2htmlEX"]