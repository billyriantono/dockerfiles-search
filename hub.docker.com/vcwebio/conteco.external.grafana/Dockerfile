##### BEGIN external-mapped/Dockerfile/iamge-header #####
FROM grafana/grafana:6.3.5
##### END external-mapped/Dockerfile/image-header #####

##### BEGIN image/Dockerfile/build-instructions #####
USER root
RUN apt-get update && apt-get install -y gettext && apt-get install -y jq && rm -rf /var/cache/apt/*
#USER grafana
##### END image/Dockerfile/build-instructions #####

##### BEGIN external/Dockerfile/conteco #####
COPY ./ /conteco/repo/
##### END external/Dockerfile/conteco #####

##### BEGIN external-mapped/Dockerfile/labels-footer #####
LABEL io.vcweb.schema-version="1.0" \
      io.vcweb.realm="vcwebio" \
      io.vcweb.ecosystem="conteco" \
      io.vcweb.type="external" \
      io.vcweb.name="grafana" \
      io.vcweb.tag="6.3.5" \
      io.vcweb.base="grafana/grafana:6.3.5" \
      io.vcweb.build="external-mapped" \
      io.vcweb.label="external.grafana - ContEco" \
      io.vcweb.description="Grafana image with ContEco external prerequisites installed." \
      io.vcweb.repository="/conteco/repo" 
##### END external-mapped/Dockerfile/labels-footer #####
