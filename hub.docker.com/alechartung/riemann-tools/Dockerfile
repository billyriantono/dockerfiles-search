FROM debian

RUN apt-get update && apt-get install -y ruby ruby-dev build-essential zlib1g-dev procps && \
    gem install --no-ri --no-rdoc riemann-tools

COPY entrypoint.sh /entrypoint.sh
RUN chmod a+x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
