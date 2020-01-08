FROM node:10

RUN apt-get -y update \
  && apt-get -y --no-install-recommends install ruby ruby-dev locales \
  && echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen \
  && locale-gen en_US.UTF-8 \
  && echo "gem: --no-document" > ~/.gemrc \
  && gem install bundler \
  && bundle config --global silence_root_warning 1 \
  && rm -rf /var/lib/apt/lists/* /tmp/* ~/.gem/

ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
