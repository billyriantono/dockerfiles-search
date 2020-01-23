FROM ruby@sha256:8acbb8041b77536dc5e8d6490d262f56042449300310e0734916bd0c338d29f0
RUN gem install --no-ri --no-rdoc fpm
RUN apt-get update && apt-get install -y rpm
ENTRYPOINT ["/usr/local/bundle/bin/fpm"]
