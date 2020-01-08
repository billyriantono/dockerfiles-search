FROM debian:9

# Install curl
RUN apt-get --quiet update
RUN apt-get -y install curl zip

# Java
ENV JAVA_FILE             jdk-10.0.1_linux-x64_bin.tar.gz
ENV JAVA_URL              http://download.oracle.com/otn-pub/java/jdk/10.0.1+10/fb4372174a714e6b8c52526dc134031e/$JAVA_FILE
ENV JAVA_VERSION          10.0.1

# Install java
# https://www.digitalocean.com/community/tutorials/how-to-manually-install-oracle-java-on-a-debian-or-ubuntu-vps
RUN curl -#LO --header "Cookie: oraclelicense=accept-securebackup-cookie" $JAVA_URL
RUN mkdir -p /opt/jdk 
RUN tar -zxf $JAVA_FILE -C /opt/jdk 
RUN rm $JAVA_FILE 
RUN update-alternatives --install /usr/bin/java java /opt/jdk/jdk-${JAVA_VERSION}/bin/java 100 
RUN update-alternatives --install /usr/bin/javac javac /opt/jdk/jdk-${JAVA_VERSION}/bin/javac 100 
ENV JAVA_HOME             /opt/jdk/jdk-${JAVA_VERSION}/

# Create user
RUN groupadd -r minecraft --gid=1000 
RUN useradd -r -g minecraft --uid=1000 minecraft

# Setup useful environment variables
ENV MINECRAFT_HOME              /minecraft
ENV MINECRAFT_JAR               /server.jar

RUN mkdir -p /minecraft

RUN curl -#LO https://launcher.mojang.com/mc/game/1.12.2/server/886945bfb2b978778c3a0288fd7fab09d315b25f/server.jar
RUN chmod 755 $MINECRAFT_JAR
RUN chown minecraft: $MINECRAFT_JAR

COPY docker-entrypoint.sh /

RUN chown minecraft: docker-entrypoint.sh
RUN chmod 700 docker-entrypoint.sh

EXPOSE 25565
VOLUME ["/minecraft"]

ENTRYPOINT ["/docker-entrypoint.sh"]