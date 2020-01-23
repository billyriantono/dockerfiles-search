FROM google/cloud-sdk:latest

RUN apt-get update && apt-get -q -y install curl xvfb libgtk-3-0 unzip
RUN curl -o /tmp/archi.tgz https://www.archimatetool.com/downloads/4.4.0/Archi-Linux64-4.4.0.tgz \
    && tar -xzf /tmp/archi.tgz -C /opt \
    && curl -o /tmp/plugin.zip https://www.archimatetool.com/downloads/plugins/org.archicontribs.modelrepository_0.5.1.201904031126.zip \
    && unzip /tmp/plugin.zip -d /opt/Archi/plugins -x archi-plugin

