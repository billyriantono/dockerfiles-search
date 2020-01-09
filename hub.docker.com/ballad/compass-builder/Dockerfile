FROM alpine:3.8

RUN set -ex \
    && apk add --update --no-cache ruby \
    && apk add --update --no-cache --virtual build-dependencies \
        build-base \
        ruby-dev \
        libffi-dev \
    && gem install --no-document \
        json \
        compass \
    && apk del build-dependencies

RUN apk add --update curl bash git

# Install jfrog client
RUN curl -fL https://getcli.jfrog.io | sh && \
    mv jfrog /usr/local/bin && \
    chmod a+x /usr/local/bin/jfrog

ENTRYPOINT ["compass"]
