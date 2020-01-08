FROM python:2.7.15-alpine

# Add GIT and SSH
RUN apk --update add git openssh && \
    rm -rf /var/lib/apt/lists/* && \
    rm /var/cache/apk/*

# Add BASH and CURL and libxml2-utils
RUN apk add --update \
        bash \
        curl \
        libxml2-utils \
    && rm -rf /var/cache/apk/*

CMD ["/bin/bash"]
