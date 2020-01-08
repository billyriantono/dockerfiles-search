FROM kapost/rbenv
MAINTAINER Kapost Engineering <noreply@kapost.com>

# Install ruby
RUN rm -Rf /tmp/*
RUN rbenv install 2.2.0 && \
    rbenv global 2.2.0 && \
    echo 'gem: --no-rdoc --no-ri' >> /$HOME/.gemrc 

# Install Bundler for each version of ruby
RUN gem install bundler && \
    rbenv rehash && \
    bundle --version && \
    ruby --version && \ 
    rbenv install 2.2.0-dev && \
    rbenv rehash
