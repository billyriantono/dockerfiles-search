FROM ruby

MAINTAINER m-takuj@sarlos.jp

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        libicu-dev cmake \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
RUN gem install gollum
RUN gem install github-markdown gollum-rugged_adapter asciidoctor

EXPOSE 80
VOLUME /wiki
WORKDIR /wiki

COPY entrypoint.sh /

ENTRYPOINT ["/entrypoint.sh"]
CMD ["--emoji", "--allow-uploads", "--show-all", "--css"]
