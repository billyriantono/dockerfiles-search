FROM dgageot/java8
MAINTAINER David Gageot <david@gageot.net>

# Install maven 3.1.1
#
RUN wget -q -O - http://apache.crihan.fr/dist/maven/maven-3/3.1.1/binaries/apache-maven-3.1.1-bin.tar.gz | tar xzf - -C /
ENV PATH $PATH:/apache-maven-3.1.1/bin

# Minimal warmup of maven
#
RUN mkdir /tmp/warmup \
	&& cd /tmp/warmup \
	&& echo "<project><modelVersion>4.0.0</modelVersion><groupId>warmup</groupId><artifactId>warmup</artifactId><version>0.1-SNAPSHOT</version><properties><project.build.sourceEncoding>UTF-8</project.build.sourceEncoding></properties></project>" > pom.xml \
	&& mvn clean install dependency:go-offline \
	&& rm -Rf /tmp/warmup

WORKDIR /home
CMD ["mvn"]
