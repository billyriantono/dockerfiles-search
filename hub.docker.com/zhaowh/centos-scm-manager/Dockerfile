FROM zhaowh/centos-java

RUN yum install -y  mercurial git subversion  &&  yum clean all

RUN mkdir /opt/scm-manager  && \
    cd  /opt/scm-manager  && \
    wget  http://maven.scm-manager.org/nexus/content/repositories/releases/sonia/scm/scm-server/1.38/scm-server-1.38-app.tar.gz  && \
    tar -xzf $(ls | grep ".gz") && \
    rm $(ls | grep ".gz")

ENV SCM_HOME /data
WORKDIR /data
VOLUME ["/data"]

EXPOSE 8080

CMD ["/opt/scm-manager/scm-server/bin/scm-server"]
