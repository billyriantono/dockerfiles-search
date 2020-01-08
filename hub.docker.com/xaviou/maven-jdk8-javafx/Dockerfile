FROM maven:3.6.1-jdk-8

RUN apt-get update && \
	apt-get install --no-install-recommends -y --force-yes fakeroot && \
    apt-get install --no-install-recommends -y --force-yes openjfx && \
    apt-get clean && \
    rm -f /var/lib/apt/lists/*_dists_*
	
RUN cp /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/ext/jfxrt.jar /usr/local/openjdk-8/jre/lib/ext && \ 
    cp /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/javafx.properties /usr/local/openjdk-8/jre/lib && \
    cp /usr/lib/jvm/java-8-openjdk-amd64/jre/lib/jfxswt.jar /usr/local/openjdk-8/jre/lib && \
    cp /usr/lib/jvm/java-8-openjdk-amd64/lib/ant-javafx.jar /usr/local/openjdk-8/lib && \
    cp /usr/lib/jvm/java-8-openjdk-amd64/lib/javafx-mx.jar /usr/local/openjdk-8/lib 
