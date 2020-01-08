# vim:set ft=dockerfile:
FROM ruby:slim

MAINTAINER Andrius Kairiukstis <andrius@kairiukstis.com>

ENV LANG=en_US.UTF-8
ENV LANGUAGE=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8
ENV TERM screen-256color

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update \
&& apt-get -yqq install \
     tzdata \
     locales \
     make \
     gcc \
     g++ \
&& echo "Europe/Barcelona" > /etc/timezone \
&& dpkg-reconfigure -f noninteractive tzdata \
&& sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen \
&& sed -i -e 's/# en_GB.UTF-8 UTF-8/en_GB.UTF-8 UTF-8/' /etc/locale.gen \
&& echo 'LANG="en_US.UTF-8"'>/etc/default/locale \
&& dpkg-reconfigure --frontend=noninteractive locales \
&& update-locale LANG=en_US.UTF-8 \
&& gem install t --no-rdoc --no-ri \
&& gem cleanup \
&& rm -rf /usr/lib/ruby/gems/*/cache/* \
&& apt-get -yqq purge make gcc g++ \
&& apt-get -yqq autoremove \
&& apt-get clean all \
&& rm -rf /var/lib/apt/lists/* /usr/share/doc /usr/share/man* /tmp/* /var/tmp/*

ENV DEBIAN_FRONTEND=interactive

ADD docker-entrypoint.sh /docker-entrypoint.sh

EXPOSE 9001

ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["/usr/local/bundle/bin/t"]

