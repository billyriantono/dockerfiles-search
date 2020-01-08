FROM            debian:stable
MAINTAINER	    Robbert Rijkse

# Install SOGo from repository
RUN apt-get update

RUN apt-get install -y --no-install-recommends apt-transport-https gnupg2 dirmngr sudo cron

COPY inverse.key /inverse.key

RUN apt-key add /inverse.key && rm /inverse.key
RUN echo "deb http://packages.inverse.ca/SOGo/nightly/4/debian/ stretch stretch" > /etc/apt/sources.list.d/inverse.list

RUN apt-get update
RUN apt-get install -y --no-install-recommends sogo sope4.9-gdl1-mysql sope4.9-gdl1-postgresql postgresql-client mysql-client
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

# Move SOGo's data directory to /srv
RUN usermod --home /srv/lib/sogo sogo
RUN mkdir -p /var/run/sogo
RUN chown sogo:sogo /var/run/sogo

# Add script
COPY sogo.sh /etc/sogo.sh
RUN chown sogo:sogo /etc/sogo.sh
RUN chmod ug+x /etc/sogo.sh

# Interface the environment
VOLUME /srv/WebServerResources/
EXPOSE 20000

# Start sogo process
ENTRYPOINT ["/bin/bash","/etc/sogo.sh"]
