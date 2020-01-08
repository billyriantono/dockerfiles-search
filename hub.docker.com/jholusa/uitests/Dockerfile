FROM fedora

RUN dnf -y update && dnf clean all
RUN dnf -y install initscripts xorg-x11-server-Xvfb wget git tar gzip java java-devel && dnf clean all

# set JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-openjdk

# set installed Maven version
ENV MAVEN_VERSION 3.2.5

# Download and install Maven
RUN curl -sSL http://archive.apache.org/dist/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar xzf - -C /usr/share \
&& mv /usr/share/apache-maven-$MAVEN_VERSION /usr/share/maven \
&& ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

# Download an install Firefox
RUN wget ftp://rpmfind.net/linux/fedora/linux/releases/27/Everything/x86_64/os/Packages/f/firefox-57.0-0.8.fc27.x86_64.rpm && dnf -y install firefox-57.0-0.8.fc27.x86_64.rpm && dnf clean all

RUN dnf -y --nogpgcheck install https://dl.google.com/linux/direct/google-chrome-stable_current_x86_64.rpm

ENV M2_HOME /usr/share/maven

