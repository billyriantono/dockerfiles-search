FROM ubuntu:18.04

MAINTAINER Tremolo Security, Inc. - Docker <docker@tremolosecurity.com>

ENV BUILDER_VERSION=1.0 \
    JDK_VERSION=1.8.0  

LABEL io.k8s.description="Builder for MyVD" \
      io.k8s.display-name="MyVirtualDirectory" \
      io.openshift.expose-services="10389:10636" \
      io.openshift.tags="ldap,virtual directory,identity management" 

RUN apt-get update;apt-get -y install curl openjdk-8-jdk-headless wget unzip;apt-get -y upgrade;apt-get clean;rm -rf /var/lib/apt/lists/*; \ 
    mkdir -p /etc/myvd && \
    mkdir -p /etc/myvd-local && \
    mkdir -p /usr/local/myvd && \
    groupadd -r myvd -g 433 && \
    useradd -u 431 -r -g myvd -d /usr/local/myvd -s /sbin/nologin -c "MyVD Docker image user" myvd && \
    mkdir -p /usr/local/myvd/work && \
    mkdir -p /usr/local/myvd/bin 

ADD run_myvd.sh /usr/local/myvd/bin/run_myvd.sh


RUN chown -R myvd:myvd \
    /etc/myvd \
    /etc/myvd-local \
    /usr/local/myvd \
  && chmod +x /usr/local/myvd/bin/*


USER 431

EXPOSE 10389
EXPOSE 10636

CMD ["usage"]
