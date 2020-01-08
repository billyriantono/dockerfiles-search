FROM centos:latest
MAINTAINER Webdroid

ENV NIKTO_VERSION 2.1.5
ENV PATH /opt/nikto:$PATH

RUN yum -y update \
&& yum -y install perl perl-Net-SSLeay openssl wget \
&& yum clean all \
&& mkdir -p /opt /workdir \
&& cd /opt \
&& wget http://www.cirt.net/nikto/nikto-${NIKTO_VERSION}.tar.gz \
&& tar xfvz nikto-${NIKTO_VERSION}.tar.gz \
&& rm -fr nikto-${NIKTO_VERSION}.tar.gz \
&& cd nikto-${NIKTO_VERSION} \
&& ln -sF /opt/nikto-${NIKTO_VERSION} /opt/nikto \
&& ln -s /opt/nikto/nikto.conf /etc/nikto.conf \
&& sed -i -e "s/UPDATES=yes/UPDATES=auto/g" /etc/nikto.conf \
&& sed -i -e "s/.*PROMPTS=no.*/PROMPTS=no/g" /etc/nikto.conf \
&& sed -i -e "s/.*EXECDIR=.*/EXECDIR=\/opt\/nikto/g" /etc/nikto.conf \
&& adduser -s /bin/bash nikto \
&& chown -R nikto /workdir \
&& chmod a+x /opt/nikto/nikto.pl \
&& ln -s /opt/nikto/nikto.pl /usr/local/bin/nikto \
&& nikto -update

USER nikto

VOLUME /workdir
WORKDIR /workdir

ENTRYPOINT ["nikto"]

CMD ["-h"]
