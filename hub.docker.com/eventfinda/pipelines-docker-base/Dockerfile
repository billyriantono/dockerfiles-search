FROM php:7.2-cli-alpine3.7

LABEL maintainer="Eventfinda Developers <dev@eventfindahq.com>"

ADD install-composer.sh install-composer.sh

RUN apk add --no-cache ca-certificates python \
    # install composer
    && ./install-composer.sh \
    # install AWS cli tools
    && wget -q https://s3.amazonaws.com/aws-cli/awscli-bundle.zip \
    && unzip -q awscli-bundle.zip \
    && rm awscli-bundle.zip \
    && ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws \
    && rm -r awscli-bundle \
    && rm -r /var/cache/apk \
    && rm -r /usr/share/man \
    && rm install-composer.sh

CMD ["php", "--version" ]