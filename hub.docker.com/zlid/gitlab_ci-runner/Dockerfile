FROM realyze/ubuntu-node-sshd
MAINTAINER Yuriy Safargaliev nekto.ryadom@gmail.com
RUN apt-get install -y wget curl gcc libxml2-dev libxslt-dev libcurl4-openssl-dev libreadline6-dev libc6-dev libssl-dev make build-essential zlib1g-dev openssh-server git-core libyaml-dev postfix libpq-dev libicu-dev vim
RUN mkdir /tmp/ruby && cd /tmp/ruby && curl --progress http://cache.ruby-lang.org/pub/ruby/2.0/ruby-2.0.0-p353.tar.bz2 | tar xj
RUN cd /tmp/ruby/ruby-2.0.0-p353 && ./configure --disable-install-rdoc && make && make install
RUN gem install bundler
RUN git clone https://github.com/Ensequence/gitlab-ci-runner.git /usr/local/gitlab_ci-runner && cd /usr/local/gitlab_ci-runner
RUN cd /usr/local/gitlab_ci-runner && bundle install
ADD .ssh /root/.ssh

RUN chown -R root:root /root/.ssh
EXPOSE 222:22
CMD ["/usr/sbin/sshd", "-D"]