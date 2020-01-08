FROM peterjc/ubuntu

MAINTAINER Peter Juhl Christiansen <mail@peterjc.dk>

RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN apt-get update && \
    gpg --keyserver hkp://keys.gnupg.net --recv-keys D39DC0E3 && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN \curl -ksSL https://get.rvm.io | bash -s stable --ruby
RUN /bin/bash -l -c "gem install bundler --no-ri --no-rdoc"
## not needed it seems
# RUN /bin/bash -l -c "gem install json_pure --no-ri --no-rdoc"
ENV PATH /usr/local/rvm/bin:/usr/local/rvm/rubies/default/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
