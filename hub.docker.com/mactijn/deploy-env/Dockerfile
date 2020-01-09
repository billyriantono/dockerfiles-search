FROM docker:git

COPY scripts /scripts
RUN apk update \
 && apk add --no-cache bash jq bc py-pip \
 && pip install docker-compose \
 && chmod 0755 /scripts/*

ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/scripts

CMD ["/bin/bash"]
