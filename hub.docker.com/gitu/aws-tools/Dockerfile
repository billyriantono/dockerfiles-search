FROM alpine:latest

RUN apk update && apk upgrade && \
    apk -v --no-cache --update add \
        python \
        py-pip \
        groff \
        less \
        mailcap \
        bash \
        git \
        openssh \
        zip \
        docker \
        && \
    pip install --upgrade awscli s3cmd python-magic
RUN addgroup -g 1000 -S circleci && \
    adduser -u 1000 -S circleci -G circleci

USER circleci:circleci
RUN umask 0077; mkdir $HOME/.ssh


