FROM debian:wheezy

ENV JRE_MAJOR 7u67
ENV JRE_VERSION $JRE_MAJOR-b01
ENV JRE_MD5SUM f6e81b9be4c1e15d59eb21e564a8973d
ENV JAVA_HOME /usr/local/lib/jvm/oracle-$JRE_VERSION

RUN apt-get update && apt-get install -y curl --no-install-recommends \
 && curl -L -H "Cookie: oraclelicense=accept-securebackup-cookie" -k "http://download.oracle.com/otn-pub/java/jdk/$JRE_VERSION/server-jre-$JRE_MAJOR-linux-x64.tar.gz" -o jre.tar.gz \
 && echo "$JRE_MD5SUM  jre.tar.gz" | md5sum -c /dev/stdin \
 && mkdir -p $JAVA_HOME \
 && tar -xzf jre.tar.gz -C $JAVA_HOME --strip-components=1 \
 && rm jre.tar.gz* \
 && apt-get purge -y --auto-remove curl \
 && rm -rf /var/lib/apt/lists/*

ENV PATH $PATH:$JAVA_HOME/bin