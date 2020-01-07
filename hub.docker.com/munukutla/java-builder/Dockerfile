FROM ubuntu
RUN apt update
RUN apt install -y wget unzip
WORKDIR /apps

RUN wget -O openjdk.tar.gz https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u222-b10/OpenJDK8U-jdk_x64_linux_hotspot_8u222b10.tar.gz
RUN tar -xvf openjdk.tar.gz --one-top-level=openjdk --strip-components=1
RUN rm openjdk.tar.gz

RUN wget -O maven.tar.gz http://apachemirror.wuchna.com/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz
RUN tar -xvf maven.tar.gz --one-top-level=maven --strip-components=1
RUN rm maven.tar.gz

RUN wget -O gradle.zip https://services.gradle.org/distributions/gradle-5.6.1-bin.zip
RUN unzip gradle.zip
RUN rm gradle.zip
RUN mv gradle-5.6.1 gradle

RUN wget -O ant.tar.gz http://apachemirror.wuchna.com//ant/binaries/apache-ant-1.10.6-bin.tar.gz
RUN tar -xvf ant.tar.gz --one-top-level=ant --strip-components=1
RUN rm ant.tar.gz

ENV PATH="$PATH:/apps/openjdk/bin:/apps/gradle/bin:/apps/maven/bin:/apps/ant/bin"
ENV HOME /root
WORKDIR $HOME
