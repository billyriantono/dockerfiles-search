FROM jenkins/jenkins:lts

SHELL ["/bin/bash", "-c"]

ENV PATH /usr/local/rvm/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:$PATH
ENV DEBIAN_FRONTEND=noninteractive

USER root

# Install needed dependencies
RUN apt-get update && apt-get upgrade -y 
RUN apt-get install -y autoconf bison build-essential libssl-dev \
    libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev \
    libgdbm3 libgdbm-dev 
RUN apt-get install -y php php-cli php-pear php-xml php-bcmath php-mcrypt \
    php-zip php-bz2 php-mbstring php-xsl
RUN apt-get install -y gnupg2 dirmngr

# Setup the Composer installer
RUN curl -o /tmp/composer-setup.php https://getcomposer.org/installer \
  && curl -o /tmp/composer-setup.sig https://composer.github.io/installer.sig \
  && php -r "if (hash('SHA384', file_get_contents('/tmp/composer-setup.php')) !== trim(file_get_contents('/tmp/composer-setup.sig'))) { unlink('/tmp/composer-setup.php'); echo 'Invalid installer' . PHP_EOL; exit(1); }"

RUN php /tmp/composer-setup.php --no-ansi --install-dir=/usr/local/bin --filename=composer && \
    rm -rf /tmp/composer-setup.php


# Prepare for rvm install
RUN groupadd rvm && \
    usermod -a -G rvm jenkins

RUN gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB

RUN curl -sSL https://get.rvm.io | bash -s stable
RUN echo 'source /etc/profile.d/rvm.sh' >> /etc/profile
RUN echo 'source /usr/local/rvm/scripts/rvm' >> /etc/profile
RUN echo 'source /etc/profile.d/rvm.sh' >> /etc/bash.bashrc
RUN echo 'source /usr/local/rvm/scripts/rvm' >> /etc/bash.bashrc
RUN /usr/local/rvm/bin/rvm requirements
RUN rvm install 2.5.1

USER jenkins

# RUN echo "[[ -s /usr/local/rvm/scripts/rvm ]] && source /usr/local/rvm/scripts/rvm" | tee /var/jenkins_home/.bashrc
RUN bash -l -c "rvm use --default 2.5.1"

RUN bash -l -c "gem install --no-rdoc --no-ri capistrano"
RUN bash -l -c "gem install --no-rdoc --no-ri bundler"

ENTRYPOINT ["/sbin/tini", "--", "/usr/local/bin/jenkins.sh"]