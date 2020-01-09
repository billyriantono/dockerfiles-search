FROM centos:7
MAINTAINER Bronius Motekaitis <bronius@praxent.com>

# Set the locale
# RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
#    locale-gen
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US:en
ENV LC_ALL en_US.UTF-8

RUN yum -y update && yum -y install centos-release-scl && yum -y groupinstall 'Development Tools'
RUN yum -y update && yum -y install \
    wget \
    git \
    automake \
    libssl-devel \
    zip \
    curl \
    ruby \
    ruby-devel \
    rubygems \
    fontconfig freetype freetype-devel fontconfig-devel libstdc++
RUN echo $(ruby -v)

RUN curl -sL https://rpm.nodesource.com/setup_0.10 | bash -
RUN yum -y install nodejs
RUN npm install -g bower && \
    npm install -g grunt-cli && \
    npm install -g node-sass
#RUN echo date.timezone="America/Chicago" >> /usr/local/etc/php/conf.d/php.ini
#RUN curl -sS https://getcomposer.org/installer | php && \
#    mv composer.phar /bin/composer
RUN gem install bundler rubygems-bundler --no-rdoc --no-ri
RUN wget -qO- https://github.com/casperjs/phantomjs-builds/archive/v1.9.8.tar.gz | tar xzv -C /tmp
RUN mv /tmp/phantomjs-builds-1.9.8/bin/phantomjs /usr/local/bin
RUN echo $(phantomjs --version)
# RUN bundle config --global silence_root_warning 1
RUN gem regenerate_binstubs
