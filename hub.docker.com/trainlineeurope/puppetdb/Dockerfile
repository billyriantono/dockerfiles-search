FROM ubuntu:xenial

ENV \
PUPPET_DB_VERSION="5.1.3" \
PUPPET_DB_DATABASE_CONNECTION="//postgres:5432/puppetdb" \
PUPPET_DB_USER=puppetdb \
PUPPET_DB_PASSWORD=puppetdb \
PUPPET_DB_JAVA_ARGS="-Djava.net.preferIPv4Stack=true -Xms256m -Xmx256m" \
PATH=${PATH}:/opt/puppetlabs/server/bin:/opt/puppetlabs/puppet/bin:/opt/puppetlabs/bin

RUN \
apt-get update && \
apt-get install -y curl lsb-release && \
curl -s https://apt.puppetlabs.com/puppet5-release-$(lsb_release -cs).deb -o puppet-release.deb && \
dpkg -i puppet-release.deb && \
rm puppet-release.deb && \
apt-get update && \
apt-get install -y --no-install-recommends puppetdb=${PUPPET_DB_VERSION}-1$(lsb_release -cs) && \
apt-get clean && \
rm -rf /var/lib/apt/lists/* /etc/puppetlabs/puppetdb/conf.d /etc/puppetlabs/puppet/auth.conf /etc/puppetlabs/puppet/hiera.yaml /etc/puppetlabs/pxp-agent /etc/puppetlabs/mcollective /etc/puppetlabs/code

ADD conf.d/puppetdb.default /etc/default/puppetdb
ADD conf.d/*.ini conf.d/*.conf /etc/puppetlabs/puppetdb/conf.d/
ADD conf.d/*.xml /etc/puppetlabs/puppetdb/logging/

EXPOSE 8081

ADD docker-*.sh /
ADD docker-entrypoint.d/* /docker-entrypoint.d/

HEALTHCHECK --interval=10s --timeout=10s --retries=90 CMD /docker-healthcheck.sh

ENTRYPOINT [ "/docker-entrypoint.sh" ]
CMD [ "puppetdb", "foreground" ]
