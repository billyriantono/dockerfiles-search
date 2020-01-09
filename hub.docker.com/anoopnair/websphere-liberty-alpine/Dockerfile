FROM alpine

ENV WLP_HOME /etc/wlp
ENV JAVA_HOME /usr/lib/jvm/java-1.8-openjdk
ENV PATH $JAVA_HOME/bin:$PATH
ENV PATH $WLP_HOME/bin:$PATH

RUN rm -rf /var/cache/apk/* && \
    rm -rf /tmp/* && \ 
   apk --update add bash wget ca-certificates sudo openssh rsync openjdk8

ADD wlp.tar.gz /etc/
RUN chmod -R o+x $WLP_HOME

VOLUME ["$WLP_HOME/config"]

EXPOSE 9080