FROM centos

ENV GITVER=2.9.5
ENV RUBYVER=2.5.0

USER root
RUN yum install -y https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
RUN yum install -y \
      docker-client \
      wget \
      https://packages.chef.io/files/stable/inspec/1.48.0/el/7/inspec-1.48.0-1.el7.x86_64.rpm \
      gcc \
      make \
      curl-devel \
      expat-devel \
      gettext-devel \
      openssl-devel \
      zlib-devel \
      zlib-devel perl-ExtUtils-MakeMaker \
      ansible \
      ansible-lint \
      ansible-review \
      standard-test-roles \
      rpm-build \
      python2-ansible-tower-cli \
      jq \
      python2-jenkins-job-builder \
      PyYAML \
      zlib \
      gcc-c++ \
      patch \
      readline \
      readline-devel \
      libyaml-devel \
      libffi-devel \
      bzip2 \
      autoconf \
      automake \
      libtool \
      bison \
      curl \
      sqlite-devel

USER root
RUN cd /usr/src && \
      wget https://www.kernel.org/pub/software/scm/git/git-${GITVER}.tar.gz && \
      tar xvf git-${GITVER}.tar.gz && \
      cd git-${GITVER} && \
      make prefix=/usr/local/git all && \
      make prefix=/usr/local/git install && \
      echo "export PATH=$PATH:/usr/local/git/bin" >> /etc/bashrc && \
      source /etc/bashrc && \
      git --version && \
      rm -f /usr/src/git-${GITVER}.tar.gz && \
      rm -rf /usr/src/git-${GITVER} && \
      cd $HOME && \
      git clone git://github.com/sstephenson/rbenv.git .rbenv && \
      git clone https://github.com/rbenv/ruby-build.git $HOME/.rbenv/plugins/ruby-build && \
      echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> $HOME/.bash_profile && \
      echo 'eval "$(rbenv init -)"' >> $HOME/.bash_profile && \
      source $HOME/.bash_profile && \
      rbenv install -v ${RUBYVER} && \
      rbenv global ${RUBYVER} && \
      ruby -v && \
    gem install puppet && \
      gem install rspec-puppet \
      serverspec \
      puppet-lint \
      puppet-syntax \
      puppetlabs_spec_helper \
      rake \
      rspec \
      rspec-puppet \
      ansible_spec_plus && \
      curl -fsSL https://goss.rocks/install | sh
