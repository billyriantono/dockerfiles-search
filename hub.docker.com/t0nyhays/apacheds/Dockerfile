FROM t0nyhays/java8base

RUN apt-get update && apt-get install -y xinetd ldap-utils procps

ADD http://apache.tradebit.com/pub//directory/apacheds/dist/2.0.0-M19/apacheds-2.0.0-M19-amd64.deb /tmp/installer.deb

RUN \
    dpkg -i /tmp/installer.deb &&\
    rm -rf /tmp/installer.deb &&\
    apt-get clean &&\
    rm -rf /var/lib/apt/lists/*

EXPOSE 10389 10636

ENTRYPOINT /opt/apacheds-2.0.0-M19/bin/apacheds console default
