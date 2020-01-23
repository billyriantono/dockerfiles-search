FROM debian:stretch
MAINTAINER JAGM <code@ongoing.today>

# Perl settings -n to don't to tests
ENV RT_FIX_DEPS_CMD /usr/bin/cpanm
ENV PERL_CPANM_OPT -n

# Config Postfix
RUN echo mail > /etc/hostname; \
    echo "postfix postfix/main_mailer_type string Internet site" > \
        preseed.txt && \
    echo "postfix postfix/mailname string mail.example.com" >> \
        preseed.txt && \
    debconf-set-selections preseed.txt && \
## Install tools and libraries
    apt-get update -yqq && \
    apt-get install -yqq --no-install-recommends \
        build-essential \
        ca-certificates \
        cpanminus \
        curl \
        git \
        gpgv2 \
        gnupg \
        graphviz \
        make \
        libexpat1-dev \
        default-libmysqlclient-dev \
        libgd-dev \
        libssl-dev \
        libdbd-mysql-perl \
        libnet-ldap-perl \
        libcache-cache-perl \
        lighttpd \
        openssl \
        perl \
        postfix \
        ssl-cert \
        cron \
        amqp-tools \
        supervisor && \
# Create user and group
    groupadd -r rt-service && \
    useradd -r -g rt-service -G www-data rt-service && \
    usermod -a -G rt-service www-data && \
    mkdir -p --mode=750 /opt/rt4 && \
    chown rt-service:www-data /opt/rt4 && \
    unlink /usr/local/man  && \
    mkdir -p /tmp/rt && \
    curl -SL https://download.bestpractical.com/pub/rt/release/rt.tar.gz | \
        tar -xzC /tmp/rt && \
    cd /tmp/rt/rt* && \
    echo "o conf init " | \
        perl -MCPAN -e shell && \
    cpan install inc::Module::Install && \
    cpan install inc::Module::Package && \
    cpan install Parse::BooleanLogic  && \
    ./configure \
        --enable-graphviz \
        --enable-gd \
        --enable-gpg \
        --with-web-handler=fastcgi \
        --with-bin-owner=rt-service \
        --with-libs-owner=rt-service \
        --with-libs-group=www-data \
        --with-db-type=mysql \
        --with-web-user=www-data \
        --with-web-group=www-data \
        --prefix=/opt/rt4 \
        --with-rt-group=rt-service && \
    make fixdeps && \
    make testdeps && \
    make config-install dirs files-install fixperms instruct && \
    cpanm git://github.com/gbarr/perl-TimeDate.git && \
# Clean up
    apt-get remove -y git cpanminus build-essential && \
    apt-get autoremove -y && \
    apt-get clean && \
    apt-get autoclean && \
    rm -rf /var/lib/apt/lists/* && \
    rm -rf /root/.cpan && \
    rm -rf /root/.cpanm && \
    rm -rf /preseed.txt /usr/share/doc && \
    rm -rf /tmp/rt/ && \
    rm -rf /usr/local/share/man /var/cache/debconf/*-old

# Copy files to docker
COPY entrypoint.sh /entrypoint.sh
COPY wrapper.sh /root/wrapper.sh
COPY 89-rt.conf /etc/lighttpd/conf-available/89-rt.conf
COPY supervisord.conf /etc/supervisor/supervisord.conf

RUN chmod +x /entrypoint.sh && \
    chmod +x /root/wrapper.sh && \
    /usr/sbin/lighty-enable-mod rt && \
    chmod 770 /opt/rt4/etc && \
    chmod 660 /opt/rt4/etc/RT_SiteConfig.pm && \
    chown rt-service:www-data /opt/rt4/var && \
    chmod 0770 /opt/rt4/var && \
    touch /opt/rt4/var/log/rt.log && \
    chown www-data:www-data /opt/rt4/var/log/rt.log

EXPOSE 80

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisor/supervisord.conf"]
