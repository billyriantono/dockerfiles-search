FROM ubuntu:16.04
MAINTAINER chenzj

RUN \
  apt-get update && \
  apt-get install -y curl libicu-dev cmake && \
  gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 && \
  curl -sSL https://get.rvm.io | bash -s stable && \
  echo "source /etc/profile.d/rvm.sh" >> /root/.bashrc && \
  /bin/bash --login -c "rvm requirements; rvm install 2.3.0; \
  /usr/local/rvm/rubies/ruby-2.3.0/bin/gem install gollum --no-ri --no-rdoc && \
  /usr/local/rvm/rubies/ruby-2.3.0/bin/gem install gollum-rugged_adapter --no-ri --no-rdoc && \
  /usr/local/rvm/rubies/ruby-2.3.0/bin/gem install redcarpet github-markdown && \
  mkdir /root/wikidata && \
  apt-get clean && \
  rm -rf /var/cache/apt/archives/* /var/lib/apt /var/lib/dpkg /var/lib/cache /var/lib/log"

ENV PATH /usr/local/rvm/gems/ruby-2.3.0/bin:/usr/local/rvm/gems/ruby-2.3.0@global/bin:/usr/local/rvm/rubies/ruby-2.3.0/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/local/rvm/bin
ENV rvm_bin_path=/usr/local/rvm/bin rvm_path=/usr/local/rvm rvm_prefix=/usr/local GEM_HOME=/usr/local/rvm/gems/ruby-2.3.0 GEM_PATH=/usr/local/rvm/gems/ruby-2.3.0:/usr/local/rvm/gems/ruby-2.3.0@global RUBY_VERSION=ruby-2.3.0 rvm_version=1.27.0\ (latest)

EXPOSE 4567

ENTRYPOINT ["gollum", "/root/wikidata", "--adapter", "rugged"]
