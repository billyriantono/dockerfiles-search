FROM codesignal/ubuntu-base:v5.0

RUN add-apt-repository -y ppa:linuxuprising/java \
    && apt-get update \
    && echo oracle-java12-installer shared/accepted-oracle-license-v1-2 select true | /usr/bin/debconf-set-selections \
    && apt-get install -y --no-install-recommends \
        oracle-java12-installer \
        oracle-java12-set-default \
        libjackson2-core-java \
        libjackson2-databind-java \
        libmysql-java \
        maven \
    && rm -rf /var/lib/apt/lists/*

# install gradle
RUN apt-get update \
    && apt-get install -y --no-install-recommends unzip \
    && wget https://services.gradle.org/distributions/gradle-5.4.1-bin.zip -P /opt/ \
    && unzip /opt/gradle-5.4.1-bin.zip -d /opt/gradle \
    && apt-get remove -qq -y unzip \
    && apt-get autoremove -qq -y \
    && apt-get autoclean \
    && rm /opt/gradle-5.4.1-bin.zip \
    && rm -rf /var/lib/apt/lists/*

# install maven
RUN wget https://www-us.apache.org/dist/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz -P /opt/ \
    && mkdir /opt/maven \
    && tar -xzf /opt/apache-maven-3.6.1-bin.tar.gz -C /opt/maven --strip-components 1 \
    && apt-get autoremove -qq -y \
    && apt-get autoclean \
    && rm /opt/apache-maven-3.6.1-bin.tar.gz \
    && rm -rf /var/lib/apt/lists/*

ENV CLASSPATH=/usr/share/java/*:$CLASSPATH \
    M2_HOME=/opt/maven \
    MAVEN_HOME=/opt/maven \
    PATH=$M2_HOME/bin:/opt/gradle/gradle-5.4.1/bin:$PATH
