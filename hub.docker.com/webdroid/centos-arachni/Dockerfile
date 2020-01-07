FROM centos:latest

ENV ARACHNI_MAIN_VERSION 1.5.1
ENV ARACHNI_VERSION ${ARACHNI_MAIN_VERSION}-0.5.12
ENV PATH /opt/arachni/bin:$PATH

RUN yum -y update \
&& yum -y install epel-release \
&& yum -y install bash wget ruby \
&& yum clean all \
&& mkdir -p /opt \
&& cd /opt \
&& wget https://github.com/Arachni/arachni/releases/download/v${ARACHNI_MAIN_VERSION}/arachni-${ARACHNI_VERSION}-linux-x86_64.tar.gz \
&& tar xfvz arachni-${ARACHNI_VERSION}-linux-x86_64.tar.gz \
&& rm -fr arachni-${ARACHNI_VERSION}-linux-x86_64.tar.gz \
&& ln -sF /opt/arachni-${ARACHNI_VERSION} /opt/arachni \
&& adduser -d /workdir -s /bin/bash arachni \
&& chown -R arachni: /workdir \
&& chown -R arachni: /opt/arachni-${ARACHNI_VERSION}

user arachni

VOLUME /workdir
WORKDIR /workdir

EXPOSE 9292

ENTRYPOINT ["/opt/arachni/bin/arachni_web", "-o", "0.0.0.0"]
