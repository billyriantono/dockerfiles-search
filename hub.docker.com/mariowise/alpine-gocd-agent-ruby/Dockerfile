FROM webcenter/alpine-gocd-agent:17.3.0-1

MAINTAINER Mario López (mario@platan.us)

RUN echo "http://dl-cdn.alpinelinux.org/alpine/edge/testing" >> /etc/apk/repositories

RUN apk add --update \
  bash ca-certificates libxml2 libxslt gcc libstdc++ \
  tzdata build-base libxml2-dev libxslt-dev libffi libffi-dev \
  nodejs imagemagick sqlite-dev postgresql-dev mysql-dev \
  cloudfoundry-cli openssh \
  ruby ruby-bundler ruby-dev ruby-irb ruby-rake \
  ruby-io-console ruby-bigdecimal ruby-json \
  ruby-bundler ruby-rdoc \
  && rm -rf /var/cache/apk/* \
  && gem install bundler \
  && gem install nokogiri

RUN ssh-keygen -a 100 -t ed25519 -q -f /root/.ssh/id_rsa -P ""

VOLUME ["/data"]
CMD ["/init"]