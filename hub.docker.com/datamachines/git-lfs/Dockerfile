FROM alpine

LABEL maintainer Rion Dooley <riondooley@datamachines.io>

COPY docker-entrypoint.sh /docker-entrypoint.sh

RUN apk --update --no-cache add git openssh-client git-lfs bash && \
    chmod +x /docker-entrypoint.sh && \	
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /var/cache/apk/*

VOLUME /git
WORKDIR /git

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["--help"]
