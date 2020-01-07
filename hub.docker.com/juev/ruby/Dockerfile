FROM ubuntu:latest
MAINTAINER Denis Evsyukov <denis@evsyukov.org>
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get install -y curl
RUN curl -sL https://deb.nodesource.com/setup | bash - \
  && apt-get install -y \
# Install build-tools
    autoconf \
    build-essential \
    zlib1g-dev \
# Install ruby
    ruby \
    ruby-dev \
# Install gsl
    gsl-bin libgsl0-dev ruby-gsl \
# Install nodejs
    nodejs \
  && rm -rf /var/lib/apt/lists/*

# copy config files
COPY copy/ /

# prepare user
RUN useradd -m -s /bin/bash user \
  && mkdir -p /srv/work \
  && rm /home/user/.bash_logout \
  && cp ~/.bashrc /home/user/.bashrc \
  && chown user.user /home/user/.bashrc \
  && chown user.user /home/user /srv/work \
  && chmod og-rwx /etc/sudoers
# install bundler
RUN gem install bundler therubyracer pry --no-ri --no-rdoc

# prepare work dir
WORKDIR /srv/work
EXPOSE 4000
USER user

# skip installing gem documentation
RUN echo 'gem: --no-rdoc --no-ri' >> "$HOME/.gemrc"
# install gems localy
ENV GEM_HOME ./vendor/bundle
ENV PATH $GEM_HOME/bin:$PATH
RUN bundle config --global path "$GEM_HOME" \
  && bundle config --global bin "$GEM_HOME/bin"
# don't create ".bundle" in all our apps
ENV BUNDLE_APP_CONFIG $GEM_HOME
ENV BUNDLE_DISABLE_SHARED_GEMS '1'
CMD [ "irb" ]
