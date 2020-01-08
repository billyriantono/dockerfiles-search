##### BEGIN external-mapped/Dockerfile/iamge-header #####
FROM docker.elastic.co/beats/metricbeat:7.1.1
##### END external-mapped/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/build-instructions #####
USER root
RUN yum install -y gettext && yum install -y epel-release && yum install -y jq && rm -rf /var/cache/yum/*
#USER filebeat
##### END image/Dockerfile/build-instructions #####

##### BEGIN external/Dockerfile/conteco #####
COPY ./ /conteco/repo/
##### END external/Dockerfile/conteco #####

##### BEGIN external-mapped/Dockerfile/labels-footer #####
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="external" \
      io.vcweb.name="metricbeat" \
      io.vcweb.tag="7.1.1" \
      io.vcweb.base="docker.elastic.co/beats/metricbeat:7.1.1" \
      io.vcweb.build="external-mapped" \
      io.vcweb.label="external.metricbeat - ContEco" \
      io.vcweb.description="ElasticSearch Metricbeat image with ContEco external prerequisites installed." \
      io.vcweb.repository="/conteco/repo" 
##### END external-mapped/Dockerfile/labels-footer #####
