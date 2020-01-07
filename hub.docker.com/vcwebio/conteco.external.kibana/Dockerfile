##### BEGIN external/Dockerfile/iamge-header #####
FROM kibana:7.1.1
##### END external/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/build-instructions #####
USER root
RUN rm -rf /usr/share/kibana/plugins/x-pack && yum install -y gettext && yum install -y epel-release && yum install -y jq && rm -rf /var/cache/yum/*
##### END image/Dockerfile/build-instructions #####

##### BEGIN external/Dockerfile/conteco #####
COPY ./ /conteco/repo/
##### END external/Dockerfile/conteco #####

##### BEGIN external/Dockerfile/labels-footer #####
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="external" \
      io.vcweb.name="kibana" \
      io.vcweb.tag="7.1.1" \
      io.vcweb.base="kibana:7.1.1" \
      io.vcweb.build="external" \
      io.vcweb.label="external.kibana - ContEco" \
      io.vcweb.description="ElastSearch Kibana image with ContEco external prerequisites installed." \
      io.vcweb.repository="/conteco/repo" 
##### END external/Dockerfile/labels-footer #####
