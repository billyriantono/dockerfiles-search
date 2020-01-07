FROM tomcat:9-jre8

MAINTAINER João Antonio Ferreira <joao.parana@gmail.com>

ENV REFRESHED_AT 2017-10-18

# Esta imagem implementa Tomcat9, Java 8, Java 9, 
# Maven, OpenSSL e Scala 2.11 sobre Debian 9 (Stretch)

# RUN apt-get update && apt-get upgrade -y gnupg

ENV SCALA_HOME /usr/local/share/scala
ENV PATH $PATH:$SCALA_HOME/bin

ENV SCALA_VERSION 2.11.11

RUN wget --quiet https://downloads.lightbend.com/scala/$SCALA_VERSION/scala-$SCALA_VERSION.tgz && \
    tar -xf scala-$SCALA_VERSION.tgz && \
    rm scala-$SCALA_VERSION.tgz && \
    mv scala-$SCALA_VERSION $SCALA_HOME

RUN apt-get update && apt-get install -y maven software-properties-common && mvn -version && which mvn

ENV JAVA_HOME  /usr/lib/jvm/java-9-oracle     
ENV PATH       ~/bin:$JAVA_HOME/bin:$PATH

# Tomcat 9 Default port 8080 conflits with Apex
RUN sed -i -E "s/8080/1443/g" $CATALINA_HOME/conf/server.xml
RUN echo '---- cat $CATALINA_HOME/conf/server.xml  ----' && \
    cat $CATALINA_HOME/conf/server.xml | grep 1443

# Para compilar fontes Java com encoding UTF-8
ENV JAVA_TOOL_OPTIONS "-Dfile.encoding=UTF8"

WORKDIR $CATALINA_HOME
# LCDS RTMP channel
EXPOSE 2037
# Tomcat web container
EXPOSE 1443
EXPOSE 80

# Install Java 9

RUN echo "••• $PATH ••• " && env | grep JAVA && mkdir /tmp/install-java-jdk9

ADD jdk9-parts /tmp/install-java-jdk9

RUN ls -lA /tmp/install-java-jdk9 && cd /tmp/install-java-jdk9 && \
    cat xa? > jdk-9.0.1_linux-x64_bin.tar && \
    tar -xf jdk-9.0.1_linux-x64_bin.tar && \
    rm jdk-9.0.1_linux-x64_bin.tar && \
    rm xa? 

RUN ls -lA /tmp/install-java-jdk9/jdk-9.0.1 && \
    mkdir -p /usr/lib/jvm/java-9-oracle && \
    mv /tmp/install-java-jdk9/jdk-9.0.1/* /usr/lib/jvm/java-9-oracle

WORKDIR /tmp 

######  RUN echo "deb http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee /etc/apt/sources.list.d/webupd8team-java.list; \
######      echo "deb-src http://ppa.launchpad.net/webupd8team/java/ubuntu xenial main" | tee -a /etc/apt/sources.list.d/webupd8team-java.list; \
######      apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys EEA14886; \
######      apt-get update
######  
######  RUN echo "`date` - Terminou o update. Iniciando intalação do Java 9" && \
######      echo oracle-java9-installer shared/accepted-oracle-license-v1-1 select true | debconf-set-selections && \
######      apt-get install -y oracle-java9-installer oracle-java9-set-default libelf-dev && \
######      rm -rf /var/cache/oracle-jdk9-installer
######  

RUN echo "••• $PATH ••• "


# Default to UTF-8 file.encoding
ENV LANG C.UTF-8

# Horário GMT-0 idioma inglês para servidor
RUN echo "Europe/London" > /etc/timezone
RUN ls -lat /etc
RUN cat /etc/timezone

WORKDIR $CATALINA_HOME/conf

RUN SUBJECT="/C=BR/ST=Rio de Janeiro/L=Rio de Janeiro/O=labdeq.cepel.br/CN=labdeq.cepel.br/emailAddress=soma@cepel.br" && \
    openssl genrsa -out ca.key 4096 && \
    openssl req -new -x509 -days 1826 -key ca.key -out ca.crt -subj "${SUBJECT}" && \
    openssl genrsa -out ia.key 4096 && \
    openssl req -new -key ia.key -out ia.csr  -subj "${SUBJECT}" && \
    openssl x509 -req -days 730 -in ia.csr -CA ca.crt -CAkey ca.key -set_serial 01 -out ia.crt

# RUN openssl pkcs12 -export -out ia.p12 -inkey ia.key -in ia.crt -chain -CAfile ca.crt

RUN cd $CATALINA_HOME && \
    echo "`date` - ••• Verificando se o APR foi instalado e configurado corretamente no Tomcat 9" && \
    catalina.sh configtest > /tmp/check-apr-instalation.txt && \
    cat /tmp/check-apr-instalation.txt && \
    echo "Verifique se houve erro"

CMD ["/bin/bash"]
