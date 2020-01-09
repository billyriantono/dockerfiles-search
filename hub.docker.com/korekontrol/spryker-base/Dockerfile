# Base container for running Spryker app in production
# It contains PHP-FPM, PHP-CLI and Jenkins

FROM korekontrol/spryker-php:php7.1

RUN  apt-get -qy update \
  && apt-get -qy --no-install-recommends install net-tools daemon procps openjdk-8-jre-headless python-jinja2 \
  && wget -q -O /tmp/jenkins.deb https://jenkins.korekontrol.net/get/package/jenkins_1.651.3_all.deb \
  && dpkg -i /tmp/jenkins.deb \
  && rm -f /tmp/jenkins.deb \
  && rm -rf /var/lib/apt/lists/* \
