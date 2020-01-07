FROM centos:6
LABEL maintainer="myugan59@gmail.com"

ENV TZ=Asia/Jakarta

# general
RUN yum -y update
RUN yum install -y sudo git nano curl wget net-tools gnupg gnupg2 locales

# set timezone
RUN cp /usr/share/zoneinfo/$TZ /etc/localtime

# Install java
RUN yum install -y java-1.8.0-openjdk.x86_64

# Install elasticsearch
ADD etc/yum.repos.d/elasticsearch.repo /etc/yum.repos.d/elasticsearch.repo
RUN yum update && yum install -y elasticsearch

# config elastic
ADD etc/default/elasticsearch /etc/default/elasticsearch
ADD etc/elasticsearch/elasticsearch.yml /etc/elasticsearch/elasticsearch.yml
RUN chown -R elasticsearch:elasticsearch /var/lib/elasticsearch /var/run/elasticsearch/ /usr/share/elasticsearch/

# install elastic plugin
RUN /usr/share/elasticsearch/bin/plugin install analysis-phonetic
RUN /usr/share/elasticsearch/bin/plugin install analysis-icu
RUN /usr/share/elasticsearch/bin/plugin install mobz/elasticsearch-head

# create docker group and user
RUN groupadd -r -g 1002 appuser
RUN useradd -rm -d /home/appuser -s /bin/bash -u 1002 -g 1002 appuser
RUN usermod -aG wheel appuser
ADD etc/sudoers /etc/sudoers

# add entrypoint
ADD entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh

USER appuser
WORKDIR /home/appuser

EXPOSE 9200 9300
ENTRYPOINT [ "/bin/bash" , "/entrypoint.sh"]