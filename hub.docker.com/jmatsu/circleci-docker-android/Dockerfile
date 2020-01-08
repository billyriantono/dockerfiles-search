FROM circleci/android:api-27-alpha

MAINTAINER Jumpei Matsuda <jmatsu.drm@gmail.com>

RUN cd /tmp && wget -O ruby-install-0.6.1.tar.gz https://github.com/postmodern/ruby-install/archive/v0.6.1.tar.gz && \
    tar -xzvf ruby-install-0.6.1.tar.gz && \
    cd ruby-install-0.6.1 && \
    sudo make install && \
    ruby-install --cleanup ruby 2.5.1 && \
    rm -r /tmp/ruby-install-*

ENV PATH ${HOME}/.rubies/ruby-2.5.1/bin:${PATH}

RUN gem install bundler
