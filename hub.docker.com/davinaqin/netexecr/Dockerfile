FROM openjdk:8-jdk

# grab gosu for easy step-down from root
ENV GOSU_VERSION 1.7
RUN set -x \
  && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
  && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
  && export GNUPGHOME="$(mktemp -d)" \
  && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
  && gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
  && rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
  && chmod +x /usr/local/bin/gosu \
  && gosu nobody true

# download elasticsearch 5.0.1
RUN cd /tmp && wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.0.1.deb
RUN dpkg -i /tmp/elasticsearch-5.0.1.deb

# set env
ENV PATH /usr/share/elasticsearch/bin:$PATH
WORKDIR /usr/share/elasticsearch

# install mvn
RUN wget http://mirrors.hust.edu.cn/apache/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
RUN tar xzvf apache-maven-3.3.9-bin.tar.gz
ENV PATH /usr/share/elasticsearch/apache-maven-3.3.9/bin:$PATH
RUN mvn -v

# install ik
RUN wget https://github.com/medcl/elasticsearch-analysis-ik/archive/v5.0.1.tar.gz
RUN tar zxvf v5.0.1.tar.gz
RUN cd elasticsearch-analysis-ik-5.0.1 && mvn package
RUN unzip /usr/share/elasticsearch/elasticsearch-analysis-ik-5.0.1/target/releases/elasticsearch-analysis-ik-5.0.1.zip -d /usr/share/elasticsearch/plugins/ik

# build work dir
RUN set -ex \
  && for path in \
    ./data \
    ./logs \
    ./config \
    ./config/scripts \
  ; do \
    mkdir -p "$path"; \
    chown -R elasticsearch:elasticsearch "$path"; \
  done

COPY config ./config

VOLUME /usr/share/elasticsearch/data

COPY docker-entrypoint.sh /

EXPOSE 9200 9300
ENTRYPOINT ["/docker-entrypoint.sh"]
CMD ["elasticsearch"]

