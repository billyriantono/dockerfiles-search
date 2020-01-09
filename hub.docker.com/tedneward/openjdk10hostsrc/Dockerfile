FROM tedneward/openjdk9
MAINTAINER Ted Neward (ted@tedneward.com)

# May seem weird that openjdk10src depends on openjdk9; this is
# because the build for OpenJDK10 depends on a OpenJDK9 boot JDK

VOLUME ["/home"]

COPY getSource.sh /usr/local/bin
COPY configure.sh /usr/local/bin
COPY deployBuild.sh /usr/local/bin
RUN chmod +x /usr/local/bin/*.sh

ENV PATH /opt/openjdk10/bin:${PATH}
ENV JAVA_HOME /opt/openjdk10

CMD ["/bin/bash"]
