FROM alpine:3.8

LABEL maintainer "Harpo Roeder <roederharpo@protonmail.ch>"

RUN apk add openssh-client su-exec

VOLUME ["/home/isolated"]

ADD https://gist.githubusercontent.com/harporoeder/44da7137e8c31028aeba56bdf0695138/raw/entrypoint.sh /entrypoint.sh

RUN chmod u+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
