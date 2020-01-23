FROM hackyo/debian
MAINTAINER hackyo <137120918@qq.com>
ENV JAVA_HOME /usr/local/jre
ENV JRE_HOME $JAVA_HOME
ENV CLASSPATH $JAVA_HOME/lib:$CLASSPATH
ENV PATH $JAVA_HOME/bin:$PATH
ADD https://media.githubusercontent.com/media/hackyoMa/docker-jre/8/server-jre-8u221-linux-x64.tar.gz /jre/
RUN cd /jre \
    && tar xzf server-jre-8u221-linux-x64.tar.gz \
    && mv jdk1.8.0_221 /usr/local/jre \
    && cd / \
    && rm -rf jre \
    && java -version
CMD ["bash"]
