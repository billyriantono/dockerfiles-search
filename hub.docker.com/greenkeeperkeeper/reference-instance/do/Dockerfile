FROM greatbsky/xtraos:latest
MAINTAINER architect.bian
LABEL name="tether" license="MIT" build-date="20180906"

ENV VERSION 0.3.1

RUN yum update -y && cd /data/softs && wget https://github.com/OmniLayer/omnicore/releases/download/v$VERSION/omnicore-$VERSION-x86_64-linux-gnu.tar.gz && tar -zvxf omnicore-$VERSION-x86_64-linux-gnu.tar.gz  && mv omnicore-$VERSION /data/env/ && ln -s /data/env/omnicore-$VERSION/bin/omnicored /usr/bin/omnicored && ln -s /data/env/omnicore-$VERSION/bin/omnicore-cli /usr/bin/omnicore-cli && rm -rf /data/softs/*

RUN sed -i '$d' /etc/rc.local && echo 'omnicored' >> /etc/rc.local

CMD ["/etc/rc.local"]
