FROM kr3ssh/debian-pam

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update

RUN apt-get install -y \
    autoconf bison libreadline6 libreadline6-dev zlib1g zlib1g-dev libsqlite3-dev \
    build-essential libssl-dev libpq-dev libyaml-dev git curl wget nano \
    libxml2-dev libxslt1-dev

RUN apt-get clean

# Install rbenv and ruby-build
RUN git clone https://github.com/sstephenson/rbenv.git /opt/rbenv
RUN git clone https://github.com/sstephenson/ruby-build.git /opt/rbenv/plugins/ruby-build
RUN git clone https://github.com/sstephenson/rbenv-vars.git /opt/rbenv/plugins/rbenv-vars
RUN /opt/rbenv/plugins/ruby-build/install.sh
ENV PATH /opt/rbenv/bin:/opt/rbenv/shims:$PATH

RUN echo 'export PATH=$HOME/.rbenv/bin:$HOME/.rbenv/shims:/opt/rbenv/bin:/opt/rbenv/shims:$PATH' >> /etc/profile
RUN echo 'eval "$(rbenv init -)"' >> /etc/profile
