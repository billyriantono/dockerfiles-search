FROM explomus/php:7.1-cli

RUN apt-get update \
    && apt-get install -y supervisor

COPY run.sh /run.sh

RUN chmod +x /run.sh

ENTRYPOINT [ "/run.sh" ]