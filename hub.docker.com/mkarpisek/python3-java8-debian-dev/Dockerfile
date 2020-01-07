FROM python:3.7

# JDK
RUN apt-get update && \
	apt-get install --no-install-recommends -y software-properties-common && \ 
	add-apt-repository -y ppa:openjdk-r/ppa && \
	apt-get install --no-install-recommends -y openjdk-8-jdk && \
	rm -rf /var/lib/apt/lists/*

# MAVEN
ENV MAVEN_VERSION 3.6.0
RUN curl -f -L http://central.maven.org/maven2/org/apache/maven/apache-maven/$MAVEN_VERSION/apache-maven-$MAVEN_VERSION-bin.tar.gz | tar -C /opt -xzv
ENV M2_HOME /opt/apache-maven-$MAVEN_VERSION
ENV maven.home $M2_HOME
ENV M2 $M2_HOME/bin
ENV PATH $M2:$PATH

# PYTHON LIBS
COPY requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

CMD ["python3"]
