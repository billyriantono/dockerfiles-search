FROM debian:wheezy

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get -qq update \
&& apt-get -qq -y --no-install-recommends install \
    build-essential \
    ruby \
    ruby-dev \
	zlib1g-dev \
&& gem install --no-ri --no-rdoc \
    jekyll \
    github-pages \
    therubyracer \
&& mkdir /data \
&& apt-get purge -y \
    build-essential \
    ruby-dev \
	zlib1g-dev \
&& apt-get autoremove -y \
&& apt-get clean \
&& rm -Rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

EXPOSE 4000

VOLUME /data

WORKDIR /data

ENTRYPOINT ["jekyll"]
