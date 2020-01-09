FROM sonatype/nexus3:3.15.2
USER root
RUN mkdir -p /opt/sonatype/nexus/system/net/staticsnow/nexus-repository-apt/1.0.9/
COPY nexus-repository-apt-1.0.9.jar /opt/sonatype/nexus/system/net/staticsnow/nexus-repository-apt/1.0.9/
COPY nexus-core-feature-3.15.2-01-features.xml /opt/sonatype/nexus/system/org/sonatype/nexus/assemblies/nexus-core-feature/3.15.2-01/nexus-core-feature-3.15.2-01-features.xml
USER nexus
