FROM bobey/docker-gitlab-ci-runner
MAINTAINER  Dustin Thomson "dthomson@51systems.com"


# Install HHVM, composer
RUN export DEBIAN_FRONTEND=noninteractive && set -x \
    && apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0x5a16e7281be7a449 \
    && echo "deb http://dl.hhvm.com/ubuntu $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/hhvm.list \
    && apt-get update -y \
    && apt-get install -y \
        hhvm \
    && /usr/bin/update-alternatives --install /usr/bin/php php /usr/bin/hhvm 60 \
    && curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin/ --filename=composer

# Cleanup apt
RUN apt-get clean
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*