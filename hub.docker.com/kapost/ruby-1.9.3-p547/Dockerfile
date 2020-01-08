FROM kapost/rbenv
MAINTAINER Kapost Engineering <noreply@kapost.com>

# Install ruby
RUN rbenv install 1.9.3-p547 && \
    rbenv global 1.9.3-p547 && \
    echo 'gem: --no-rdoc --no-ri' >> /$HOME/.gemrc 

# Install Bundler for each version of ruby
RUN gem install bundler && \
    rbenv rehash && \
    bundle --version && \
    ruby --version && \ 
    rbenv install 1.9.3-dev && \
    rbenv rehash
RUN curl --silent --location https://deb.nodesource.com/setup_0.12 | bash -
RUN apt-get install --yes nodejs
