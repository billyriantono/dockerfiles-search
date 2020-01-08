FROM hackyo/jre:8
MAINTAINER hackyo <137120918@qq.com>
ENV M2_HOME /usr/local/maven
ENV PATH $M2_HOME/bin:$PATH
ADD https://archive.apache.org/dist/maven/maven-3/3.6.1/binaries/apache-maven-3.6.1-bin.tar.gz /maven/
RUN cd /maven \
    && tar xzf apache-maven-3.6.1-bin.tar.gz \
    && mv apache-maven-3.6.1 /usr/local/maven \
    && cd / \
    && rm -rf maven \
    && sed -i '55c <localRepository>/usr/local/maven/repository</localRepository>' /usr/local/maven/conf/settings.xml \
    && sed -i '147,158c <mirror>\n<id>aliyunmaven</id>\n<mirrorOf>*</mirrorOf>\n<name>阿里云公共仓库</name>\n<url>https://maven.aliyun.com/repository/public</url>\n</mirror>' /usr/local/maven/conf/settings.xml \
    && mvn -v
CMD ["bash"]
