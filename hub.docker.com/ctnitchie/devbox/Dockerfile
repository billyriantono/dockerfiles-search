FROM ctnitchie/java8

MAINTAINER Chris Nitchie <chris@nitchie.com>

# Prepare for installs
RUN apt-get update

# Basics
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    man \
    sudo

# Network utilities
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y \
    ssh \
    curl \
    wget

# Set up subversion APT repository
RUN wget -q -O - http://opensource.wandisco.com/wandisco-debian.gpg | apt-key add - && \
    echo "deb http://opensource.wandisco.com/debian/ wheezy svn17" > /etc/apt/sources.list.d/wandisco-subversion.list && \
    apt-get update

# Version control
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    mercurial \
    subversion \
    subversion-tools \
    git

# Text editors
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    vim \
    nano

# Build Tools
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y \
    ant \
    maven

# Node.js and common modules
RUN curl -sL https://deb.nodesource.com/setup | bash -
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y nodejs
RUN npm install -g less coffee-script uglify-js underscore express mocha handlebars mustache

# Docker
RUN curl -sSL https://get.docker.com/ubuntu/ | sh

# Ruby and common gems
RUN DEBIAN_FRONTEND=noninteractive apt-get install --no-install-recommends -y ruby ruby-dev
RUN gem install sass

# Add config files
ADD hgrc /home/dev/.hgrc
ADD bashrc /home/dev/.bashrc
ADD splash /etc/splash
ADD entrypoint.sh /usr/bin/entrypoint.sh
RUN chmod a+x /usr/bin/entrypoint.sh

# Set up 'dev' user and let it sudo without password
RUN adduser -q --system --disabled-password --gecos '' --uid 1000 dev && \
    adduser dev sudo && \
    echo "dev ALL=(ALL) NOPASSWD:ALL">>/etc/sudoers.d/dev-sudo && \
    chown -R dev:nogroup /home/dev/

VOLUME /data
VOLUME /home/dev
WORKDIR /data
USER dev
ENTRYPOINT ["/usr/bin/entrypoint.sh"]
CMD bash
