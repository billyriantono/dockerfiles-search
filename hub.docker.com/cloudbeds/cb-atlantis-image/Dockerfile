FROM runatlantis/atlantis:v0.8.3

ENV AWSCLI_VERSION "1.14.10"

RUN apk add --update \
    python \
    python-dev \
    py-pip \
    build-base \
    && pip install awscli==$AWSCLI_VERSION --upgrade

COPY atlantis.yml /opt/atlantis.yml
COPY new-docker-entrypoint.sh /usr/local/bin/new-docker-entrypoint.sh
RUN chmod 755 /usr/local/bin/new-docker-entrypoint.sh

ENTRYPOINT ["/usr/local/bin/new-docker-entrypoint.sh"]
CMD ["server"]
