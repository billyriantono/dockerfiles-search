FROM evarga/jenkins-slave:latest

ENV DEBIAN_FRONTEND=noninteractive

RUN echo "jenkins:$(head /dev/urandom | tr -dc A-Za-z0-9 | head -c 13 ; echo '')" | chpasswd

RUN echo 'APT::Install-Recommends "0";\nAPT::Install-Suggests "0";\nAPT::Get::Assume-Yes "true";\nAPT::Get::force-yes "true";' > /etc/apt/apt.conf.d/01norecommend-and-yes

RUN apt-get update && apt-get upgrade
RUN apt-get install python-yaml \
    python-jinja2 \
    python-httplib2 \
    python-keyczar \
    python-paramiko \
    python-setuptools \
    python-pkg-resources
RUN apt-get install libgconf-2-4 \
    libssl-dev \
    libffi-dev \
    python-dev
RUN apt-get install git \
    wget \
    curl \
    telnet \
    vim \
    unzip \
    rsync
RUN apt-get install python-pip \
    build-essential

RUN apt-get install chromium-browser \
    chromium-chromedriver \
    && ln -s /usr/bin/chromium-browser /usr/bin/google-chrome \
    && ln -s /usr/lib/chromium-browser/chromedriver /usr/bin/chromedriver

# see https://stackoverflow.com/a/34047383/490502 for `/var/lib/dpkg/info/ca-certificates-java.postinst configure`
RUN apt-get install maven \
    ca-certificates-java \
    openjdk-8-jdk-headless \
    && /var/lib/dpkg/info/ca-certificates-java.postinst configure

RUN cd ~ \
    && wget https://cache.ruby-lang.org/pub/ruby/2.5/ruby-2.5.1.tar.gz \
    && tar -xvf ruby-2.5.1.tar.gz \
    && cd ruby-2.5.1 \
    && ./configure \
    && make \
    && make install \
    && cd ~

RUN echo "gem: --no-ri --no-rdoc" > ~/.gemrc \
    && gem install bundler \
    && gem install capistrano          --version=2.6.0 \
    && gem install capistrano-ext      --version=1.2.1 \
    && gem install railsless-deploy    --version=1.1.3 \
    && gem install sshkit              --version=1.9.0 \
    && gem install i18n                --version=0.7.0

RUN mkdir -p /etc/ansible/ /var/jenkins-agent
RUN echo '[local]\nlocalhost\n' > /etc/ansible/hosts
RUN chown -R jenkins:jenkins /etc/ansible/ /var/jenkins-agent
RUN pip install --upgrade setuptools
RUN pip install ansible virtualenv
RUN virtualenv /home/jenkins/pyenv3
RUN chown -R jenkins:jenkins /home/jenkins/pyenv3
RUN rm -rf /var/lib/apt/lists/*
