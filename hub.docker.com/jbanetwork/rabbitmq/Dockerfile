FROM alpine:3.4

RUN echo "@testing http://nl.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories && \
    apk add --update --no-cache \
        rabbitmq-server@testing \
        erlang-public-key \
        erlang-asn1 \
        bash

ENV RABBITMQ_LOGS=- RABBITMQ_SASL_LOGS=-
ENV PATH /usr/lib/rabbitmq/bin:$PATH
ENV HOME /var/lib/rabbitmq

COPY rabbitmq /etc/rabbitmq
COPY docker-entrypoint.sh /usr/bin/docker-entrypoint.sh

RUN chown -R rabbitmq:rabbitmq /etc/rabbitmq

EXPOSE 4369 5671 5672 25672 15672

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["rabbitmq-server"]