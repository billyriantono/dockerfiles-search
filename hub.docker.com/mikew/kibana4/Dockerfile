FROM centos:centos7
MAINTAINER Mike Wells

RUN yum -y install tar && yum clean all

RUN useradd kibana
RUN chown kibana /opt
USER kibana

COPY entrypoint.sh /opt/entrypoint.sh

ENV version=4.0.3
RUN cd /opt/ && curl -O https://download.elasticsearch.org/kibana/kibana/kibana-${version}-linux-x64.tar.gz && tar xvf kibana-${version}-linux-x64.tar.gz && rm /opt/kibana-${version}-linux-x64.tar.gz
RUN ln -s /opt/kibana-${version}-linux-x64 /opt/kibana

EXPOSE 5601
ENTRYPOINT ["/opt/entrypoint.sh"]
