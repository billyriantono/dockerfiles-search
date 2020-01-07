FROM rabbitmq:management

RUN apt-get update && apt-get install -y zsh python pcregrep

COPY ql /usr/local/bin/
COPY rabbitmqadmin /usr/local/bin/
COPY docker-healthcheck /usr/local/bin/

HEALTHCHECK CMD ["docker-healthcheck"]
