FROM ubuntu:16.04
LABEL maintainer="Kizzii <apisit.kizzii@gmail.com>"


# Timezone configurations
ENV DEBIAN_FRONTEND noninteractive
ENV DEBCONF_NONINTERACTIVE_SEEN true

# Add configuration file
COPY config-files /config-files

# Set time zone
RUN echo "tzdata tzdata/Areas select Asia" > /tmp/timezone.txt; \
    echo "tzdata tzdata/Zones/Europe select Bangkok" >> /tmp/timezone.txt; \
    debconf-set-selections /tmp/timezone.txt \
    # Install packages
    && apt-get update && apt-get install -y --fix-missing vim software-properties-common \
    && add-apt-repository -y cloud-archive:queens \
    # Install client packages
    && apt-get update && apt-get install -y --fix-missing python-openstackclient mysql-client \
    python-swiftclient python-keystoneclient \
    # Install keystone, swift and dashboard packages
    keystone apache2 libapache2-mod-wsgi swift swift-proxy \
    python-keystonemiddleware memcached rsync \
    swift-account swift-container swift-object openstack-dashboard \
    # Copy keystone config to /etc/keystone
    && mv /config-files/keystone/keystone.conf /etc/keystone/keystone.conf \
    # Copy swift config to /etc/swift
    && mv /config-files/swift/*.conf /etc/swift/ \
    && mv /config-files/swift/*.ring.gz /etc/swift/ \
    && mv /config-files/swift/*.builder /etc/swift/ \
    # Copy dashboard config to /etc/dashboard
    && mv /config-files/dashboard/* /etc/openstack-dashboard/ \
    # Copy initial scripts & admin credential to root path 
    && mv /config-files/init.sh /init.sh \
    && mv /config-files/keystone/admin.sh /admin.sh \
    # Change permission file
    && chmod +x /init.sh \
    # Remove default apache config file
    && rm /etc/apache2/sites-enabled/000-default.conf

EXPOSE 8080 5000 80

VOLUME /etc/keystone /etc/swift /etc/openstack-dashboard /srv/node

ENTRYPOINT ["./init.sh"]

CMD ["/usr/sbin/apachectl", "-DFOREGROUND"]
